
## 滴滴技术选型方法论


技术选型关键需要思考三个角度：技术、业务和人。

### 角度之一：技术

技术选型首先考虑的当然是技术本身，这里提到的技术包括语言、框架、工具、设计模式、开发模式等。

在选择技术时有两个大原则。**第一，要取其长避其短；第二，要关注技术的发展前景。**

每种技术都是有它特定的适用场景的，“没有银弹”。开发者经常犯的错误就是盲目追新，当一个新语言、框架、工具出现后，特别是开发者自己学会了这种新技术后，就会有种“拿着锤子找钉子”的感觉，将新技术滥用于各种项目。

比如最近几年 Go 在国内很火，我自己也非常使用它开发项目，但绝对不应该将它用于所有项目。Go 的优点是上手快、运行时性能高、方便的使用多核运算能力等，经常被提起的特性是超轻线程 goroutine、内置的内存队列 chan、极快的编译速度，非常适合于编写各种无状态应用服务，无需使用任何的第三方框架都能轻松写出一个高性能的 http 服务。

但它的缺点也非常明显，最痛的一点是 gc。Go 在设计之初就号称要实现一个世界上最优秀的 gc，可惜直到今天也还差的较远，最近一年才实现了 jvm 几年前就做到的并发 gc，并且没有很好的方法解决内存碎片和对象过多带来的性能问题。这些缺陷使得 Go 不太适合做有状态服务，特别不适合做内存管理相关的服务，在这些场景里面还是 C/C++ 更加可靠。

**技术的发展前景也是一个重要考虑因素**。有些技术设计的很好，比如我个人挺喜欢一个叫做 Io 的语言，但我不会把它用于真实项目，因为这个语言缺乏社区和长期支持，就算设计理念写的再好，里面也必然有各种 bug 和不足，如果没人能够解决就会带来严重的问题。技术的“前景”可以从几个维度来判断，有没有长期规划、有没有持续投入的人或者社区、问题解决的速度如何、业界使用案例及口碑、源码质量。

选择一个技术最低限的标准是，**技术的生命周期必须显著长于项目的生命周期**。想象一下，如果项目还没做完这个技术就不被维护了，那将是怎样一种窘境。拿去年很火的 Vue.js 来说，尤大在规划、投入和解决问题速度方面都没有问题，这是这个技术能火起来的基本保障，再加上设计优雅、源码确实写的不错，它的成功并不偶然。可以预见，随着尤大全职开发这个框架并且社区贡献者越来越多，Vue.js 能持续几年应该问题不大。

滴滴的 web app，比如微信钱包里面的滴滴入口，就在去年年底全面改用 Vue.js 重构了一版，我们就是看中了 Vue.js 在移动应用开发中的优势再加上对它的前景有信心。在重构前，我们为了确认 Vue.js 真的能承担如此大任，公共前端团队在 2016 年花了半年的时间整体梳理和评估了 Vue.js 1.0 和 2.0 的全部源码，为此还出了一本书，在公司大规模使用前也在滴滴小巴业务和行程分享功能里做了试点，效果非常不错，最终才真正下定决心广泛推广。

**技术的发展前景是动态变化的，当一个技术走向了末路，我们也应该勇敢的扬弃**。拿 jQuery 为例，最开始它是前端开发的必需品，当时很多前端同学离开了 $ 函数就不会写代码了，它在简化 DOM 操作、抹平浏览器间差异做出了极其重要的贡献。但是随着浏览器越来越标准和趋同，jQuery 的亮点已经不再吸引人，它的插件开发模式逐步被模块化开发给取代，再加上各种历史包袱，它所适用的项目也会变得越来越少，新项目在选型的时候就不推荐优先考虑 jQuery 了。

对于一家大型公司来说，其核心业务的技术选型更需谨慎，看前景时甚至需要考虑技术的独立性。依然把 Go 当做一个例子，当前核心 Go Authors 基本都受雇于 Google，也没有一个独立运作的基金会来负责语言的长期维护，更没有一个公开透明的决策机制来决定语言的未来，假如 Google 出于某种原因停止投入或者改变语言的发展方向，那么这对一家大型公司来说可能会是毁灭性打击。立志于成为一家千亿美元规模的公司，或者是 Google 的潜在竞争对手，在选择使用 Go 时就应该更加谨慎，不要盲从。

### 角度之二：业务

技术选型必须贴着业务来选择，不同业务阶段会有不同的选型方式。

**处于初创期的业务，选型的关键词是“灵活”**。只要一个技术够用且开发效率足够高，那么就可以选择它。初创的业务往往带有风险性和不确定性，朝令夕改、反复试错是常态，技术必须适应业务的节奏，然后才是其他方面。MongoDB 是一个很好的例子，相比 MySQL，它的数据结构灵活多变，相比一般的 KV 存储，它又具有类似 SQL 的复杂查询能力，再加上它内置的傻瓜式高可用和水平扩展机制，让它能够很好的适应初创业务对效率的追求。

**等业务进入稳定期，选型的关键词是“可靠”**。技术始终是业务的基石，当业务稳定了技术不稳，那就会成为业务的一块短板，就必须要修正。当年 Twitter 放弃 RoR 选择 Java 系框架，这就是个很好的例子。RoR 以快速开发著称，但同时 ruby 的性能非常有限，Twitter 工程团队针对 ruby 虚拟机做了非常多性能优化可是依然不能达到预期，再加上当时的 Twitter 为了提升前端体验，全面使用模块化和异步化的方法加载页面，服务端已经基本不怎么负责渲染页面，而专注于提供各种 RESTful API，RoR 的优势也不太明显了。

**当业务步入维护期，选型的关键词是“妥协”**。代码永远有变乱的趋势，一般经过一两年就有必要对代码来一次大一点的重构。在这种时候，必须得正视各种遗留代码的迁移成本，如果改变技术选型会带来遗留代码重写，这背后带来的代价业务无法承受，那么我们就不得不考虑在现有技术选型之上做一些小修小补或者螺旋式上升的重构。

正因为技术选型和业务相关，我们能够观察到一些很明显的现象：新技术往往被早期创业团队或大公司的新兴业务使用；中大型公司的核心业务则更倾向于用一些稳定了几年的技术；一个公司如果长期使用一种技术，就会倾向于一直使用下去，甚至连版本都不更新的使用下去。这现象背后都是有道理的。

### 角度之三：人

技术选型过程中最终影响决策的还是人本身，这里要强调一下，我说的**“人”是指的个人，而不是团队**。

**技术选型的决策流程一定得专制**。决策者可以在调研的时候体恤民情，并把团队现状当做一个因素考虑进来，但绝对不能采用类似“少数服从多数”、“按着大家习惯来”的方式选型。专制可以使技术选型更加的客观，考虑的更加全面，并且使得权责统一。

并不是每个人都懂得怎么为项目负责，一个基层的开发人员思考的更多的可能是技术是否有挑战、能否做出彩、甚至未来好不好找工作，这些主观因素可能会给选型带来灾难性的后果。专制也使得“螺旋式上升”成为可能，很多时候我们没法一蹴而就的使用某种技术，这时候需要有一个领路人，带着大家坚定的朝一条曲折的路线前进才能获得成功。

**技术选型也非常依赖于人的能力**。选型是一件很难被标准化的过程，选型的决策质量跟人的眼界、经验、业务敏感度、逻辑性等息息相关。就我自己来说，我在面临一个选型问题时首先考虑的是去学习，看看公司内外类似的问题如何解决的，避免自己闭门造车，然后思考所有的可能性，列举最核心需要考虑的因素，心里列一个方案优劣对比，最后将这些逻辑整理清楚，落地成一个决策。

滴滴在决策客户端动态化方向时就是以这样的方式来进行的，我们将业界所有可能的方案都拿出来，理解他们的优缺点，然后在某次会议上几个核心同学在白板上列了一张表格，以考虑的因素为行，可能的方案为列，分别评估各个方案在每种因素里的优劣势，最终确定了一个结论。我们选择的路是偏向于客户端开发的动态化方案，在保留所有代码和工具链的前提下做到对开发者透明的动态化，这样能让整体迁移和维护代价变得最小，当然，这条路开发难度也相当大，幸好我们当时也找到了最合适的人，我们依然可以在能接受的时间里实现整个方案。

**培养技术选型的能力**

可以看到，要想做好技术选型还是挺难的，要想做好得有足够的知识积累和实际踩坑的经历才行。如果一个不太懂得如何选型的新人想学着做好这件事，那可以先从小项目开始做尝试，慢慢积累经验。技术选型对人来说最重要的还是“逻辑性”，每一个决策背后都藏着许多假设和事实，我们通过不断挑战这些背后的东西来逐步成长。

比如在需要使用缓存来加快数据访问速度的场景中，我们可能会很自然的选择 redis 作为缓存服务。这看似“直觉”的决策，背后也是由一系列假设和事实组成。可以问自己一连串问题，看看在具体的场景下这个决策是不是真的正确，例如，缓存服务有没有 redis 之外的选项、是否可以在内存里直接缓存、redis 是否稳定、redis 性能是否满足需求、数据库访问速度瓶颈究竟在哪等等问题，很可能最终结果还是“ 使用 redis 做缓存”这个直观方案，但正因为有分析的过程，让我们在下一次做决策可以更迅速、更自信。

**如何保持敏感性和广度**

技术选型是个很需要经验的活，得有大量的信息积累和输入，再根据具体现实情况输出一个结果。我们在选型的时候最忌讳的是临时抱佛脚、用网上收集一些碎片知识来决策，这是非常危险的，我们得确保自己所有思考都是基于以前的事实，还要弄清楚这些事实背后的假设，这都需要让知识内化形成经验。

我一直在想，“经验”的本质是什么，有什么方法能够确定自己的经验增长了，而不是不断在重复一些很熟悉的东西。我现在的结论是，经验等于“知识索引”的完备程度。

我们一生中会积累很多的知识，如果把我们的大脑比作数据库的话，那我们一定有一部分脑存储贡献给了内容的索引，它能帮助我们将关联知识更快的取出来，并且辅助决策。经验增长等同于我们知识索引的增长，意味着我们能轻易的调动更多的关联知识来做更全面的决策。

要想建立好这个知识索引，我们得保持技术敏感性和广度，也就是要做到持续的信息输入、内化，并发现信息之间的关联性，建立索引，记下来。说起来容易，做起来还是挺有难度的。

首先难在信息输入量大，忘记了怎么办。我们的大脑不是磁盘，不常用的知识就会忘记，忘记了就跟没看过是一回事。我的经验是一定要对知识进行压缩，记住的是最关键的细节，并且反复的去回味这个细节。

比如我学习各种语言的时候就会非常留意一些最有特色的语法特性和应用场景，像 C++，我一直记得很早以前看过的细节，像编译器默认会生成哪些类方法，默认析构、拷贝构造、operator = 等，默认生成的类方法有哪些场景需要显示禁用，什么时候要在构造函数用 explicit 等，我看这些细节已经超过十五年的时间了，依然记忆尤新。

看起来好像有点难度，实际上不难，大家想想自己学过的英文单词，再怎么样最常见的几百个英文单词还是能清楚的记得含义的，而技术的知识点其实压缩之后会远小于英文单词的个数，记忆负担不会有想象中那么大。

然后难在信息更新速度太快，跟不上技术发展怎么办。我学习了非常多技术之后就会发现这确实是个难解的问题，像前端开发，每年都会有新的框架和开发方式出现，ES7 的语法如果不去提前了解，过两年可能连 Javascript 语法都看不懂了。

我在这个问题上也是有些焦虑的，不过多少还是有应对的方式，就是坚持碎片化学习，增量更新过时的内容，只要形成习惯也还是能够慢慢的找到自己的节奏。如果有些技术实在细节太多，比如 Node.js 这种，我以前曾经通读过源码，仔细研究过内部设计，但随着它不断发展现在我也不太敢说对它内部有多熟悉，那我会考虑大胆的放弃追新，等着我可能需要用它的时候再统一更新到最新的知识。

**最后难在信息究竟如何存入知识索引，知识太零散形成不了体系，建不了索引怎么办**。最入门的做法是看书，看别人是怎么将知识变成一个个章节的信息。要想掌握建立索引背后的方法论，我的经验是先从两个相近的技术开始，找到建索引的感觉，然后再铺开去学习更多知识。有这样困惑的开发者往往在学习方面有些贪心，觉得自己记性好可以囫囵吞枣式的将知识强行内化，这样做短期可以，长期还是会遗忘，也形成不了经验。

其实技术知识之间非常像，有很多共性的点可以挖掘。比如客户端和前端开发，各个框架在 View 生命周期管理、消息派发机制等方面非常像，后端开发则更加的套路化，无论用那种语言，最基本的分布式服务原理、缓存、队列、数据库等基础组件原理，都万变不离其宗。

如果我们更宏观的看每个领域，甚至于都能发现领域之间的知识体系划分也很类似。作为表现层的前端和客户端，知识体系都可以分为语言、API、工程化、框架和设计模式。比如前端的语言包括 HTML、CSS、Javascript 和一些稍小众的 TypeScript、CoffeeScript 等，API 就是各种标准、接口的使用、能够实现的效果、平台限制等，工程化就是各种打包工具、代码转化工具、辅助开发工具等，框架就是像 Vue、React 等，设计模式就是像 PWA、redux 等。

相应的，刚刚说的这些知识都能找到在 iOS 或 Android 里几乎对应的知识，无非换了一些细节，这里我就不继续展开了。服务端也是这样，知识体系最顶层的部分也很少，具体到细节，只是要了解每一个实现背后的优劣。

### 总结

总结一下，技术选型依赖于经验，经验又来源于知识索引的建设，这依赖于平时的总结和不断的新知识输入，技术是一辈子的事，必须得投入大量时间维持状态。学无止尽，大家一起共勉。


###### *作者：*

*杜欢，滴滴出行技术总监，负责滴滴小巴业务的技术管理工作。在互联网领域已经有十年工作经验，曾就职于微软、百度，也曾自主创业两次，来到滴滴之后也经历过很多项目和业务的变化，是一个“什么都懂”工程师，对前端、客户端、服务端、运维等方面都有不少实战经验。平时是一个 ACG 宅，也喜欢阅读各种技术和非技术的文章扩大视野，不愿主动交谈，但一旦放松了就聊到停不下来。*