---
layout: post
title: 对TinyOS中接口的理解
date: 2012-04-25 18:14
comments: true
categories: [Coding]
tags: [tinyos, nesc, 接口]
---

TinyOS 环境下的编程是基于组件的，组件包括配件和模块：模块负责具体的功能实现；配件负责高层次的结构管理，用来连接各个模块。
组件之间相互交互要通过接口，这是面向对象的思想的一点体现。
通常情况下模块会provides一些接口，同时会uses 一些接口。
模块如果provides接口的话，就需要实现command函数，也就是告诉别人应该怎么去use我provide的接口；相反，如果组件uses接口，那么它就必须实现event函数，来告诉别人我是如何实现的这个接口。因为command就是命令，event就是事件嘛~

其实，今天是因为一个小问题而对TinyOS中的接口有了进一步的认识：
现在有一个模块 moduleA 已经提供了interfaceA 、interfaceB 两个接口。
即

	Module moduleA {
	  	Provides {
	  
	    interface interfaceA;
	    interface interfaceB;
	  
	  	}
	  
	 	implementation{
	  	...
	  	...
	  
	  	}
	}

而在配件moduleAC中，通过绑定，使得顶层配件来提供这两个接口

如
	configuration moduleAC{
	
	  	provides {
	  	
	  	  	interface interfaceA;
	  	  	interface interfaceB;
	  	
	  	}
  	
	  	uses{}
	  	implementation{

	  		components moduleA ,...
	  	
	  	  	interfaceA = moduleA.interfaceA;
	  	 	interfaceB = moduleA.interfaceB;
	  	
	  	}
	
	}

其中interfaceA 、 interfaceB 都是Tinyos自有的接口，例如我们常见的SplitControl、AMSend 或者 Receive等等。但是现在我想要自己定义一个接口interfaceNew 然后让moduleA模块 provides这个接口。
我需要怎么做呢？
简单的在moduleA中加入 provides interfaceNew是不行的，需要自己定义一个接口。

新建interfaceNew.nc 文件
例如
	interface interfaceNew{
		command error_t function() ;
	}

仅仅这样是不够的，还需要在配件中进行说明
现在还要新建interfaceNewC.nc 文件
	configuration interfaceNewC{

		provides interfaceNew;

	}

现在，在moduleA模块中对interfaceNew接口进行具体的实现
	Module moduleA {
		provides {

			interface interfaceA;
			interface interfaceB;
			interface interfaceNew；
		}

		implementation{
		...
		...

		command error_t interfaceNew.function(){

		  ...
		  ...
		}

	}
}

最后，在moduleAC这个想要对外提供interfaceNew接口的组件中进行绑定

现在 interfaceNewC.nc中 是这个样子

	configuration moduleAC{

		provides {

			interface interfaceA;
			interface interfaceB;
			interface interfaceNew；
		}

		uses{}

		implementation{
			components moduleA ,...

			interfaceA = moduleA.interfaceA;
			interfaceB = moduleA.interfaceB;
			interfaceNew = moduleA.interfaceNew ;
		}

	}

这样，其他组件如果想要使用interfaceNew的话就需要从moduleAC这个配件中调用。

总体感觉配件提供接口就是对模块提供的接口进行进一步的封装。
