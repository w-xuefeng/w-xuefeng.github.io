---
title: 记百度前端一面
date: 2019-08-06 14:22:00
categories: 技术贴 | 面试题
tags: Javascript
thumbnail: https://pub.wangxuefeng.com.cn/asset/blogthumbnail/baiduInterview/thumbnail.png
---

2019年7月31日，这天烈日当空，骄阳似火，我孤身前往北京百度科技园，参加百度前端社招面试。

谜之自信的我，从不做面试前的准备，刷面试题对我来说是不可能的，顶多也就瞟两眼，不会花很多时间在这个上面，更愿意把时间都用来真正实践中项目中。然鹅我还是`Too young Too naive`🤦‍！

到了北京百度科技园，进入K2大厅，首先映入眼帘的是大厅中央的AI机器人，然后就是百度的Logo，环视一周，感觉不愧是百度在北京的总部，K2的大厅要比网易在北京研发中心的大厅大一点。距离约定好的面试时间还有一点时间，我被安排在右边的沙发上等待面试官。就在此时，我拿起我的荣耀手机，随手拍了一张大厅的照片。如下

<div style="width:100%;display:flex;flex-direction:column;justify-content:center;text-align:center;">

  <img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/baiduInterview/hall.jpg" style="width:100%;max-width:600px;margin: 5px auto;">

</div>

到了约定的时间，面试官带我通过门禁，进入`后堂`，前往面试的小桌边。扫视一周，发现周围全都是面试或者讨论问题的人，我，只是这芸芸众生中的一员。

接下来开始正式面试了，面试官手拿Mac，上面有我的电子简历，开始询问问题，我也开始回答问题。

还是那句话，我真的是`Too young Too naive`，面试官问的问题都是能百度到的面试题，而我就是没有去刷。虽然一些问题大概是知道的，但是原理性的东西东很模糊，回答起来都很笼统，可越是笼统的回答，面试官就越是要详细的去问，这个时候，就只能乖乖的回答*I don't Know*了，倘若稍加要蒙混过关，那么就是诚信问题了。经过这样`宁静而又祥和的`面试后，面试结果也就心知肚明了。归根到底，还是自己基础不扎实，没有追根溯源，搞明白原理。所以学习一定要有探索精神，要探究本源，弄清原理，不能糊弄自己，要对的起自己付出的时间。

好了，废话不多说，直接上题吧：

- 1.你在上一家公司实习用的什么前端框架？

  > Angular

- 2.你认为 Angular 和 Vue 各自的优缺点在什么地方？

  > Angular，出生比 Vue 早，相对 Vue 要更加"老练", 适合做大型 Web 项目。Angular 采用“脏值检测”的方式，数据发生变更后，对于所有的数据和视图的绑定关系进行一次检测，识别是否有数据发生了改变，有变化进行处理，可能进一步引发其他数据的改变，所以这个过程可能会循环几次，一直到不再有数据变化发生后，将变更的数据发送到视图，更新页面展现。

  > Vue，定位用于中小型前端项目，相对于 Angular 更加年轻。Vue 使用 Object.defineProperty() 方法，监控对数据的操作，从而可以自动触发数据同步。并且，由于是在不同的数据上触发同步，可以精确的将变更发送给绑定的视图，而不是对所有的数据都执行一次检测。

- 3.那你说说 Angular 的 “脏值检测” 吧，会不会有性能问题？

  > Angular 团队通过对 [zone.js](https://github.com/angular/angular/tree/master/packages/zone.js) 封装，实现了 脏检查机制（Change Detection 或 Dirty Checking）。
  > Angular 默认是脏检查方法是从根组件开始，遍历所有的子组件进行脏检查。
  >
  > 触发条件
  >   - Ajax 请求， 
  >   - Timeout 延迟事件，
  >   - 鼠标事件
  >
  > 触发脏检测的目的就是检测视图(DOM)有没有发生变化，方法就是比较 双向绑定中 view 和 model 是否一致。
  >
  > 脏检测的效率必然不会太高，但也不会很慢。性能优化的话，可以从
  >  + 减少逻辑代码的复杂程度
  >  + 减少 Event Handler（可做节流和防抖）
  >  + 降低 DOM 树复杂度
  > 等几方面进行。
  >
  > 具体可参考文章
  > - [如何理解angular的脏检查](https://www.jianshu.com/p/850f0f76e908)
  > - [Angular性能优化之脏检测](https://blog.csdn.net/wf19930209/article/details/83515873)

- 4.为什么说 Vue 定位于中小型前端项目，有什么例子能证明 Vue 不能做或者做不好大型项目吗？

  > Vue.js 官网这样介绍自己：
  > Vue (读音 /vjuː/，类似于 view) 是一套用于构建用户界面的渐进式框架。**与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用**。
  >
  > 具体有什么例子能证明 Vue 不能做或者做不好大型项目暂时还不太清楚，但是能确定的是 Vue 生而为“简”。与 React 的简单对比如下图所示：

  <div style="width:100%;display:flex;flex-direction:column;justify-content:center;text-align:center;">

    <img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/baiduInterview/vue&react1.png" style="width:100%;max-width:500px;margin: 5px auto;">

    <img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/baiduInterview/vue&react2.png" style="width:100%;max-width:500px;margin: 5px auto;">

    <p>（图片来自<a href="https://www.jianshu.com/p/b7cd52868e95" target="_blank">vue和react的区别之我见</a>）</p>

  </div>

  > 具体可参考
  > - [React.js与Vue.js：流行框架的比较](https://baijiahao.baidu.com/s?id=1608099200125495014&wfr=spider&for=pc)
  > - [vue和react的区别之我见](https://www.jianshu.com/p/b7cd52868e95)

- 5.说说 Vue 的双向绑定原理吧。

  > Vue.js 官网解释如下：
  >
  > 当你把一个普通的 JavaScript 对象传入 Vue 实例作为 data 选项，Vue 将遍历此对象所有的属性，并使用 Object.defineProperty 把这些属性全部转为 getter/setter。Object.defineProperty 是 ES5 中一个无法 shim 的特性，这也就是 Vue 不支持 IE8 以及更低版本浏览器的原因。
  >
  > 这些 getter/setter 对用户来说是不可见的，但是在内部它们让 Vue 能够追踪依赖，在属性被访问和修改时通知变更。这里需要注意的是不同浏览器在控制台打印数据对象时对 getter/setter 的格式化并不同，所以建议安装 vue-devtools 来获取对检查数据更加友好的用户界面。
  >
  > 每个组件实例都对应一个 watcher 实例，它会在组件渲染的过程中把“接触”过的数据属性记录为依赖。之后当依赖项的 setter 触发时，会通知 watcher，从而使它关联的组件重新渲染。

  <div style="width:100%;display:flex;flex-direction:column;justify-content:center;text-align:center;">

    <img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/baiduInterview/vue.png" style="width:100%;max-width:500px;margin: 5px auto;">
    
    <p>（图片来自<a href="https://cn.vuejs.org/v2/guide/reactivity.html" target="_blank">Vue.js 官网 深入响应式原理</a>）</p>

  </div>


  > 自己的理解：Vue 通过 Object.defineProperty() 将传入参数的 data 的属性全部转为 getter/setter。在getter/setter 的内部实现对数据监控和拦截，并结合发布者-订阅者模式，在数据变动时发布消息给订阅者，触发相应的监听回调，并更新视图。


- 6.能说说Object.defineProperty()这个方法吗，还有在 Vue 的双向绑定原理中 getter/setter 里面具体做了什么？ 

  > Object.defineProperty(obj, prop, descriptor)
  >
  > 接收三个参数，分别是
  > - obj 要在其上定义属性的对象
  > - prop 要定义或修改的属性的名称
  > - descriptor 将被定义或修改的属性描述符
  > 
  > 返回 被传递给函数的对象
  >
  > 关于 `descriptor`, 称为属性描述符，对象里目前存在的属性描述符有两种主要形式：**数据描述符**和**存取描述符**。<br>
  > **数据描述符**是一个具有值的属性，该值可能是可写的，也可能不是可写的。<br>
  > **存取描述符**是由 getter-setter 函数对描述的属性。<br>
  > **描述符必须是这两种形式之一；不能同时是两者**。
  >
  > 数据描述符和存取描述符均具有以下可选键值
  >
  >(默认值是在使用Object.defineProperty()定义属性的情况下)：
  >
  > - configurable 当且仅当该属性的 configurable 为 true 时，该属性描述符才能够被改变，同时该属性也能从对应的对象上被删除。`默认为 false`。
  > - enumerable 当且仅当该属性的enumerable为true时，该属性才能够出现在对象的枚举属性中。`默认为 false`。
  >
  > 数据描述符同时具有以下可选键值：
  > - value 该属性对应的值。可以是任何有效的 JavaScript 值（数值，对象，函数等）。`默认为 undefined`。
  > - writable 当且仅当该属性的writable为true时，value才能被赋值运算符改变。`默认为 false`。  
  > 
  > 存取描述符同时具有以下可选键值：
  >
  > - get 一个给属性提供 getter 的方法，如果没有 getter 则为 undefined。当访问该属性时，该方法会被执行，方法执行时没有参数传入，但是会传入this对象（由于继承关系，这里的this并不一定是定义该属性的对象）。`默认为 undefined`。
  > - set 一个给属性提供 setter 的方法，如果没有 setter 则为 undefined。当属性值修改时，触发执行该方法。该方法将接受唯一参数，即该属性新的参数值。`默认为 undefined`。
  >
  > **如果一个描述符不具有value,writable,get 和 set 任意一个关键字，那么它将被认为是一个数据描述符。如果一个描述符同时有(value或writable)和(get或set)关键字，将会产生一个异常**。
  >
  > 如果同时要定义或修改多个属性，可以使用 `Object.defineProperties(obj, props)` 
  > 如：
  >
  ```js
      var obj = {};
      Object.defineProperties(obj, {
        'property1': {
          value: true,
          writable: true
        },
        'property2': {
          value: 'Hello',
          writable: false
        }
        // etc. etc.
      });
  ```
  >
  > Vue 的双向绑定原理中 getter/setter 里面具体做了什么，看看源码：
  >
  > 源码来自：https://github.com/vuejs/vue/blob/dev/src/core/observer/index.js

  ```js

    // ...
    /**
    * Define a reactive property on an Object.
    */
    export function defineReactive (
      obj: Object,
      key: string,
      val: any,
      customSetter?: ?Function,
      shallow?: boolean
    ) {
      const dep = new Dep()

      const property = Object.getOwnPropertyDescriptor(obj, key)
      if (property && property.configurable === false) {
        return
      }

      // cater for pre-defined getter/setters
      const getter = property && property.get
      const setter = property && property.set
      if ((!getter || setter) && arguments.length === 2) {
        val = obj[key]
      }

      let childOb = !shallow && observe(val)
      Object.defineProperty(obj, key, {
        enumerable: true,
        configurable: true,
        get: function reactiveGetter () {
          const value = getter ? getter.call(obj) : val
          if (Dep.target) {
            dep.depend()
            if (childOb) {
              childOb.dep.depend()
              if (Array.isArray(value)) {
                dependArray(value)
              }
            }
          }
          return value
        },
        set: function reactiveSetter (newVal) {
          const value = getter ? getter.call(obj) : val
          /* eslint-disable no-self-compare */
          if (newVal === value || (newVal !== newVal && value !== value)) {
            return
          }
          /* eslint-enable no-self-compare */
          if (process.env.NODE_ENV !== 'production' && customSetter) {
            customSetter()
          }
          // #7981: for accessor properties without setter
          if (getter && !setter) return
          if (setter) {
            setter.call(obj, newVal)
          } else {
            val = newVal
          }
          childOb = !shallow && observe(newVal)
          dep.notify()
        }
      })
    }

    /**
    * Collect dependencies on array elements when the array is touched, since
    * we cannot intercept array element access like property getters.
    */
    function dependArray (value: Array<any>) {
      for (let e, i = 0, l = value.length; i < l; i++) {
        e = value[i]
        e && e.__ob__ && e.__ob__.dep.depend()
        if (Array.isArray(e)) {
          dependArray(e)
        }
      }
    }
    // ...

  ```
  > 其中 get 
  >
  ```js
    get: function reactiveGetter () {
      const value = getter ? getter.call(obj) : val
      // 判断 property 是否已经具有 getter
      // 如果已经具有 getter，则调用该 getter
      // 否则 value 为该属性值
      if (Dep.target) {
      // Dep 为一个订阅器，判断是否需要添加订阅者，也可以叫做收集依赖
        dep.depend()
        // 添加订阅者 收集依赖
        if (childOb) {
          // 如果需要添加子订阅者
          childOb.dep.depend()
          // childOb.dep 为一个子订阅器，在子订阅器添加订阅者
          if (Array.isArray(value)) {
            // 如果 value 是数组的话
            dependArray(value)
            // （递归）添加数组订阅者，监听数组的变化
          }
        }
      }
      return value
      // 返回 value
    },
   ```
  > set

  ```js
  set: function reactiveSetter (newVal) {
    const value = getter ? getter.call(obj) : val
    // 获取修改前的 value
    
    /* eslint-disable no-self-compare */
    if (newVal === value || (newVal !== newVal && value !== value)) {
    // 如果 新的值与修改前相同 直接返回
      return
    }
    /* eslint-enable no-self-compare */
    if (process.env.NODE_ENV !== 'production' && customSetter) {
    // 如果在生产环境下并且具有 customSetter， 则调用 customSetter
      customSetter()
    }
    // #7981: for accessor properties without setter
    if (getter && !setter) return
    // 如果没有 setter 访问者属性的话直接返回
    
    if (setter) {
    // 如果 property 已经有 setter，调用 setter
      setter.call(obj, newVal)
    } else {
    // 否则 进行赋值
      val = newVal
    }
    childOb = !shallow && observe(newVal)
    // （递归）更新子订阅器
    dep.notify()
    // 向订阅者发布更新，更新视图
  }
  ```
  > 源码传送门
  > - [双向绑定具体实现 源码](https://github.com/vuejs/vue/blob/dev/src/core/observer/index.js)
  > - [Watcher 的具体实现 源码](https://github.com/vuejs/vue/blob/dev/src/core/observer/watcher.js)
  > - [Dep 的具体实现 源码](https://github.com/vuejs/vue/blob/dev/src/core/observer/dep.js)
  >
  > 简单总结一下就是，在 getter 中添加订阅，收集依赖， 在 setter 中发布订阅，更新依赖和视图

- 7.说说 Vue 中 watch 和 computed 的区别。

  > - [vue 官网的解释](https://cn.vuejs.org/v2/guide/computed.html)
  > - 简单总结一下：
  >   + computed: 计算属性，用于复杂的逻辑计算，并且基于它们的响应式依赖将计算结果进行缓存以减少性能开销，如果不希望有缓存，可以使用方法来替代。计算属性默认只有 getter ，不过在需要时也可以提供一个 setter。计算属性不可在 data 里面定义, 。
  >   + watch: 侦听器, 用于在数据变化时需要执行异步或开销较大的操作时，每个 watch 具有 oldValue 和 newValue 参数；可以设置中间状态，这些都是计算属性无法做到的。
  >
  > - 具体实现 computed:
  >

  ```js
    // src/core/instance/state.js

    // 初始化计算属性
    function initComputed (vm: Component, computed: Object) {
      ...
      // 遍历 computed 计算属性
      for (const key in computed) {
        ...
        // 创建 Watcher 实例
        // create internal watcher for the computed property.
        watchers[key] = new Watcher(vm, getter || noop, noop, computedWatcherOptions)

        // 创建属性 并将提供的函数将用作属性的 getter，
        // 最终 computed 与 data 会一起混合到 vm 下，所以当 computed 与 data 存在重名属性时会抛出警告
        defineComputed(vm, key, userDef)
        ...
      }
    }

    export function defineComputed (target: any, key: string, userDef: Object | Function) {
      ...
      // 创建 get set 方法
      sharedPropertyDefinition.get = createComputedGetter(key)
      sharedPropertyDefinition.set = noop
      ...
      // 创建属性，并初始化 getter setter
      Object.defineProperty(target, key, sharedPropertyDefinition)
    }

    function createComputedGetter (key) {
      return function computedGetter () {
        const watcher = this._computedWatchers && this._computedWatchers[key]
        if (watcher) {
          if (watcher.dirty) {
            // watcher 暴露 evaluate 方法用于取值操作
            watcher.evaluate()
          }
          // 判断是否处于依赖收集状态
          if (Dep.target) {
            watcher.depend()
          }
          return watcher.value
        }
      }
    }
  ```

  > 无论是属性还是计算属性，都会生成一个对应的 watcher 实例。

  ```js
    // src/core/observer/watcher.js

    // 当获取计算属性时，就会进到这个 getter 方法
    get () {
      // this 指的是 watcher 实例
      // 将当前 watcher 实例暂存到 Dep.target，这就表示开启了依赖收集任务
      pushTarget(this)
      let value
      const vm = this.vm
      try {
        // 在执行定义计算属性的函数时，会触发属性和计算属性的 getter
        // 在这个执行过程中，就可以收集到定义计算属性的依赖了
        value = this.getter.call(vm, vm)
      } catch (e) {
        if (this.user) {
          handleError(e, vm, `getter for watcher "${this.expression}"`)
        } else {
          throw e
        }
      } finally {
        if (this.deep) {
          traverse(value)
        }
        // 结束依赖收集任务
        popTarget()
        this.cleanupDeps()
      }
      return value
    }
  ```

  > dep

  ```js
    // src/core/observer/dep.js

    export default class Dep {
      static target: ?Watcher;
      id: number;
      subs: Array<Watcher>;

      constructor () {
        this.id = uid++
        this.subs = []
      }

      addSub (sub: Watcher) {
        this.subs.push(sub)
      }

      removeSub (sub: Watcher) {
        remove(this.subs, sub)
      }

      depend () {
        if (Dep.target) {
          Dep.target.addDep(this)
        }
      }

      notify () {
        const subs = this.subs.slice()
        for (let i = 0, l = subs.length; i < l; i++) {
          // 更新 watcher 的值，与 watcher.evaluate() 类似，
          // 但 update 是给依赖变化时使用的，包含对 watch 的处理
          subs[i].update()
        }
      }
    }

    // 当首次计算 computed 属性的值时，Dep 将会在计算期间对依赖进行收集
    Dep.target = null
    const targetStack = []

    export function pushTarget (_target: Watcher) {
      // 在一次依赖收集期间，如果有其他依赖收集任务开始（比如：当前 computed 计算属性嵌套其他 computed 计算属性），
      // 那么将会把当前 target 暂存到 targetStack，先进行其他 target 的依赖收集，
      if (Dep.target) targetStack.push(Dep.target)
      Dep.target = _target
    }

    export function popTarget () {
      // 当嵌套的依赖收集任务完成后，将 target 恢复为上一层的 Watcher，并继续做依赖收集
      Dep.target = targetStack.pop()
    }    
  ```

  > 总结一下依赖收集、动态计算的流程：
  > - data 属性初始化 getter setter
  > - computed 计算属性初始化，提供的函数将用作属性的 getter
  > - 当首次获取计算属性的值时，Dep 开始依赖收集
  > - 在执行 getter 方法时，如果 Dep 处于依赖收集状态，则判定 该属性为 计算属性 的依赖，并建立依赖关系
  > - 当 所依赖的属性 发生变化时，根据依赖关系，触发 计算属性的函数 重新计算
  >
  >   参考文章：[深入理解 Vue Computed 计算属性](https://segmentfault.com/a/1190000010408657)

  > - 具体实现 watch:

  ```js
    // 初始化
    // initState -> initWatch

    function Vue(){
      ... // 其他处理
      initState(this)
      ... // 解析模板，生成DOM 插入页面
    }
    function initState (vm: Component) {
      ... // 处理 data，props，computed 等数据
      if (opts.watch && opts.watch !== nativeWatch) {
        initWatch(vm, opts.watch)
      }
    }
    function initWatch (vm: Component, watch: Object) {
      for (const key in watch) {
        const handler = watch[key]
        if (Array.isArray(handler)) {
          for (let i = 0; i < handler.length; i++) {
            createWatcher(vm, key, handler[i])
          }
        } else {
          createWatcher(vm, key, handler)
        }
      }
    }
    /**
    * Strict object type check. Only returns true
    * for plain JavaScript objects.
    */
    function isPlainObject (obj: any): boolean {
      return _toString.call(obj) === '[object Object]'
    }
    function createWatcher (
      vm: Component,
      expOrFn: string | Function,
      handler: any,
      options?: Object
    ) {
      // expOrFn 是 key，handler 可能是对象

      // 监听属性的值是一个对象，包含handler，deep，immediate
      if (isPlainObject(handler)) {
        options = handler
        handler = handler.handler
      }
      if (typeof handler === 'string') {
        handler = vm[handler]
      }
      return vm.$watch(expOrFn, handler, options)
    }
    Vue.prototype.$watch = function (
        expOrFn: string | Function,
        cb: any,
        options?: Object
      ): Function {
        // expOrFn 是 监听的 key，cb 是监听的回调，options 是 监听的所有选项
        const vm: Component = this
        if (isPlainObject(cb)) {
          return createWatcher(vm, expOrFn, cb, options)
        }
        options = options || {}
        options.user = true
        const watcher = new Watcher(vm, expOrFn, cb, options)
        if (options.immediate) {
          // 设定了立即执行，马上执行回调
          try {
            cb.call(vm, watcher.value)
          } catch (error) {
            handleError(error, vm, `callback for immediate watcher "${watcher.expression}"`)
          }
        }
        return function unwatchFn () {
          watcher.teardown()
        }
      }
    }
    class Watcher {
      // ...
      constructor (
        vm: Component,
        expOrFn: string | Function,
        cb: Function,
        options?: ?Object,
        isRenderWatcher?: boolean
      ) {
        // ...
        this.vm = vm
        this.deep = opt.deep
        this.cb = cb
        // ...
        // parse expression for getter
        if (typeof expOrFn === 'function') {
          this.getter = expOrFn
        } else {
          this.getter = parsePath(expOrFn)
          // ...
          this.value = this.lazy
            ? undefined
            : this.get()            
          // this.get 作用就是执行 this.getter 函数
      }
      // ...
      get () {
        // this 指的是 watcher 实例
        // 将当前 watcher 实例暂存到 Dep.target，这就表示开启了依赖收集任务
        pushTarget(this)
        let value
        const vm = this.vm
        try {
          // 触发 getter
          value = this.getter.call(vm, vm)
        } catch (e) {
          if (this.user) {
            handleError(e, vm, `getter for watcher "${this.expression}"`)
          } else {
            throw e
          }
        } finally {
          if (this.deep) {
            // 处理深度监听
            traverse(value)
          }
          // 结束依赖收集任务
          popTarget()
          this.cleanupDeps()
        }
        return value
      }

      /**
      * Subscriber interface.
      * Will be called when a dependency changes.
      */
      update () {
        /* istanbul ignore else */
        if (this.lazy) {
          this.dirty = true
        } else if (this.sync) {
          this.run()
        } else {
          queueWatcher(this)
        }
      }

      /**
      * Scheduler job interface.
      * Will be called by the scheduler.
      */
      run () {
        if (this.active) {
          const value = this.get()
          if (
            value !== this.value ||
            // Deep watchers and watchers on Object/Arrays should fire even
            // when the value is the same, because the value may
            // have mutated.
            isObject(value) ||
            this.deep
          ) {
            // set new value
            const oldValue = this.value
            this.value = value
            if (this.user) {
              // cb 是监听回调
              try {
                this.cb.call(this.vm, value, oldValue)
              } catch (e) {
                handleError(e, this.vm, `callback for watcher "${this.expression}"`)
              }
            } else {
              this.cb.call(this.vm, value, oldValue)
            }
          }
        }
      }
      // ...
    };

    const seenObjects = new Set()
    /**
    * Recursively traverse an object to evoke all converted
    * getters, so that every nested property inside the object
    * is collected as a "deep" dependency.
    * 递归遍历一个对象以唤起所有转换的 getter，使对象内的每个嵌套属性被收集为“深层”依赖
    */

    export function traverse (val: any) {
      _traverse(val, seenObjects)
      seenObjects.clear()
    }

    function _traverse (val: any, seen: SimpleSet) {
      let i, keys
      const isA = Array.isArray(val)
      if ((!isA && !isObject(val)) || Object.isFrozen(val) || val instanceof VNode) {
        return
      }
      if (val.__ob__) {
        const depId = val.__ob__.dep.id
        if (seen.has(depId)) {
          return
        }
        seen.add(depId)
      }

      // 不断递归深入读取对象，收集依赖
      if (isA) {
        // val[i] 就是读取值了，然后值的对象就能收集到 watch-watcher
        i = val.length
        while (i--) _traverse(val[i], seen)
      } else {
        keys = Object.keys(val)
        i = keys.length
        while (i--) _traverse(val[keys[i]], seen)
      }
    }

  ```

  > 大概总结一下
  > - 1.获取监听回调
  >   + 如果配置是个对象，就取 handler 字段
  >   + 如果配置是函数，那么直接就是 监听回调
  >   + 如果配置是字符串，从实例上获取函数
  > - 2.调用 vm.$watch
  >   + 判断是否立即执行监听回调
  >   + 每个 watch 配发 watcher
  >   + watcher 在结尾会立即执行一次 watcher.get，其中便会执行 getter，便会根据监听的 key，去实例上读取并返回，存放在 watcher.value 上
  >   + 通过 traverse 实现深度监听
  >   + 通过 watcher.update 实现更新，并调用 监听回调且传入新值和旧值
  >
  > 参考文章：[【Vue原理】Watch - 源码版](https://segmentfault.com/a/1190000019684439)

- 8.谈谈 XSS 和 CSRF 的区别。

  > XSS (Cross Site Scripting)，即跨站脚本攻击，是一种常见于 Web 应用中的计算机安全漏洞。
  > 恶意攻击者往 Web 页面里嵌入恶意的客户端脚本，当用户浏览此网页时，脚本就会在用户的浏览器上执行，进而达到攻击者的目的。
  > 比如获取用户的 Cookie、导航到恶意网站、携带木马等。借助安全圈里面非常有名的一句话：
  >
  ```
    所有的输入都是有害的。
  ```
  >
  > CSRF（Cross-site request forgery）跨站请求伪造，也被称为“One Click Attack”或者Session Riding，通常缩写为CSRF或者XSRF，是一种对网站的恶意利用。尽管听起来像跨站脚本（XSS），但它与XSS非常不同，XSS利用站点内的信任用户，而CSRF则通过伪装成受信任用户的请求来利用受信任的网站。与XSS攻击相比，CSRF攻击往往不大流行（因此对其进行防范的资源也相当稀少）和难以防范，所以被认为比XSS更具危险性。

  > 详见
  > - [简述XSS和CSRF的概念和区别](https://blog.csdn.net/weixin_39327883/article/details/89512217)
  > - [XSS及CSRF攻击防御](https://blog.csdn.net/zl834205311/article/details/81773511)

- 9.解决跨域的方式有哪些？

  > - 1.jsonp
  > - 2.PostMessage, PostMessage 是一个用于安全地使用跨源通信的方法。它允许来自不同源的脚本采用异步的方式进行有限的通信，可以实现跨文本档、多窗口、跨域消息传递，相当于提供了一个受控的机制来安全地绕过浏览器的同源限制
  > - 3.CORS，服务端设置 `header( "Access-Control-Allow-Origin:*" );`
  > - 4.代理, 开发环境下可以配置 webpack 的 devServer 下的 proxy，生产环境中可以通过配置nginx或apache等服务端程序代理转发请求

- 10.说说前端页面的性能优化吧。

  > - 1.尽量减少 HTTP 请求个数
  > - 2.使用 CDN（内容分发网络）
  > - 3.为文件头指定 Expires 或 Cache-Control ，使内容具有缓存性。
  > - 4.避免空的 src 和 href
  > - 5.使用 gzip 压缩内容
  > - 6.把 CSS 放到顶部
  > - 7.把 JS 放到底部
  > - 8.避免使用 CSS 表达式
  > - 9.将 CSS 和 JS 放到外部文件中
  > - 10.减少 DNS 查找次数
  > - 11.精简 CSS 和 JS
  > - 12.减少页面重定向
  > - 13.剔除重复的 JS 和 CSS
  > - 14.配置 ETags
  > - 15.使 AJAX 可缓存
  > - 16.尽早刷新输出缓冲
  > - 17.使用 GET 来完成 AJAX 请求
  > - 18.延迟加载
  > - 19.预加载
  > - 20.减少 DOM 元素个数
  > - 21.根据域名划分页面内容
  > - 22.尽量减少 iframe 的个数
  > - 23.避免 404
  > - 24.减少 Cookie 的大小
  > - 25.使用无 cookie 的域
  > - 26.减少 DOM 访问
  > - 27.用 `<link>` 代替 `@import`
  > - 28.避免使用滤镜
  > - 29.优化图像
  > - 30.优化 CSS Spirite
  > - 31.favicon.ico要小而且可缓存
  > - 32.保持单个内容小于25K、
  > - 等等

- 11 具体说说`预加载`和`延迟加载`。

  > - **预加载**: 预加载是一种浏览器机制，使用浏览器空闲时间来预先下载/加载用户接下来很可能会浏览的页面/资源，当用户访问某个预加载的链接时，如果从缓存命中,页面就得以快速呈现
  > - **延迟加载**：通过对`script`标签设置`defer` 或 `async`属性实现异步加载。
  >
  > - async 与 defer 的异同：
  >   + 相同点：异步加载文件
  >   + 不同点：
  >     * async：虽然是异步加载，但当有多个脚本异步加载的时候，不一定先加载哪一个，加载顺序不一定
  >     * defer：加载顺序由第一个延迟脚本到最后一个延迟脚本
  >     * Chrome下的真实情况见[浅谈script标签的defer和async](https://segmentfault.com/a/1190000006778717),
  >     ```
  >     所以，通俗来讲，chrome 浏览器首先会请求HTML文档，然后对其中的各种资源调用相应的资源加载器进行异步网络请求，同时进行DOM渲染，直到遇到 <script> 标签的时候，主进程才会停止渲染等待此资源加载完毕然后调用V8引擎对js解析，继而继续进行 DOM 解析。
  >     我的理解如果加了async 属性就相当于单独开了一个进程去独立加载和执行，而 defer 是和将 <script> 放到 <body> 底部一样的效果。  
  >     ```
- 12.了解**防抖**和**节流**吗？

  > 在前端开发的过程中，我们经常会需要绑定一些持续触发的事件，如 resize、scroll、mousemove 等等，但有些时候我们并不希望在事件持续触发的过程中那么频繁地去执行函数。 通常这种情况下防抖和节流是比较好的解决方案。
  >
  > - 防抖（debounce）: 所谓防抖，就是指触发事件后在 n 秒内函数只能执行一次，如果在 n 秒内又触发了事件，则会重新计算函数执行时间。
  ```js
    /**
    * @desc 函数防抖
    * @param func 函数
    * @param wait 延迟执行毫秒数
    * @param immediate true 表立即执行，false 表非立即执行
    */
    function debounce(func, wait, immediate) {
      let timeout;
      return function () {
        let context = this;
        let args = arguments;
        if (timeout) clearTimeout(timeout);
        if (immediate) {
          var callNow = !timeout;
          timeout = setTimeout(() => {
            timeout = null;
          }, wait)
          if (callNow) func.apply(context, args)
        } else {
          timeout = setTimeout(function(){
            func.apply(context, args)
          }, wait);
        }
      }
    }
  ```
  > - 节流（throttle）: 所谓节流，就是指连续触发事件但是在 n 秒中只执行一次函数。节流会稀释函数的执行频率。
  ```js
    /**
    * @desc 函数节流
    * @param func 函数
    * @param wait 延迟执行毫秒数
    * @param type 1 表时间戳版，2 表定时器版
    */
    function throttle(func, wait ,type) {
      if (type === 1) {
        let previous = 0;
      } else if (type===2) {
        let timeout;
      }
      return function() {
        let context = this;
        let args = arguments;
        if (type === 1) {
          let now = Date.now();
          if (now - previous > wait) {
              func.apply(context, args);
              previous = now;
          }
        } else if (type === 2) {
          if (!timeout) {
            timeout = setTimeout(() => {
              timeout = null;
              func.apply(context, args)
            }, wait)
          }
        }
      }
    }
  ```
  > 参考文章：[函数防抖和节流](https://www.jianshu.com/p/c8b86b09daf0)


- 13.Dom 的**重绘**和**回流**呢？

  > - **重绘（repaint）**: （盒子模型的宽高、位置、样式确定后）浏览器把元素绘制出来称为重绘。当前元素的样式(背景颜色、字体颜色等)发生改变的时候，我们只需要把改变的元素重新的渲染一下即可 ,重绘对浏览器的性能影响较小，所以一般不考虑。
  > - **回流（reflow）**: 当页面上的结构发生改变，浏览器会从新的渲染我们的页面，回流是比较消耗性能的。
  >   + 回流产生的情况 
  >     * 1、添加或者删除可见的DOM元素； 
  >     * 2、元素位置改变； 
  >     * 3、元素尺寸改变——边距、填充、边框、宽度和高度 
  >     * 4、内容改变——比如文本改变或者图片大小改变而引起的计算值宽度和高度改变； 
  >     * 5、页面渲染初始化； 
  >     * 6、浏览器窗口尺寸改变——resize事件发生时；
  > 由于回流 对浏览器的影响比较大，所以我们一般是用文档碎片的方式去解决这个问题的，当我们需要给DOM中添加新的元素的时候，先将其放在一个容器中，然后统一添加，这样就只产生了一次回流。

  ```js
    var frg = document.createDocumentFragment();
      // 创建了一个文档碎片:相当于一个容器，
      // 把动态创建的li先放到容器中,最后一起添加到页面中(只引发一次回流)
     for (var i = 0; i < 10; i++) {
       var oLi = document.createElement("li");
       oLi.onmouseover = function () {
         this.style.backgroundColor = "#22b909";
       }
       oLi.onmouseout = function () {
           this.style.backgroundColor = "";
       }
       frg.appendChild(oLi);
     }
     oUl.appendChild(frg);
  ```

- 14.`Promise.all()` 和 `Promise.race()` 的优缺点有哪些？
  
  > - Promise.all()
  >   + 常见使用场景 ： 多个异步结果合并到一起, Promise.all可以将多个Promise实例包装成一个新的Promise实例。用于将多个Promise实例，包装成一个新的Promise实例。
  >   + 它接受一个可迭代对象，如 Array 或 String。
  >   + 如果传入的参数是一个空的可迭代对象，则返回一个已完成（already resolved）状态的 Promise。
  >   + 如果传入的参数不包含任何 promise，则返回一个异步完成（asynchronously resolved） Promise。注意：Google Chrome 58 在这种情况下返回一个已完成（already resolved）状态的 Promise。
  >   + 其它情况下返回一个处理中（pending）的Promise。这个返回的 promise 之后会在所有的 promise 都完成或有一个 promise 失败时异步地变为完成或失败。
  >   + 返回值将会按照参数内的 promise 顺序排列，而不是由调用 promise 的完成顺序决定。
  >   + 此方法在集合多个 promise 的返回结果时很有用。
  >   + 传入的数组可以是Promise对象，也可以是其它值，只有Promise会等待状态改变。
  >   + 当所有的子Promise都完成，该Promise完成，返回值是全部值的数组。
  >   + 如果有任何一个失败，该Promise失败，返回值是第一个失败的子Promise的结果。
  >   + 在任何情况下，Promise.all 返回的 promise 的完成状态的结果都是一个数组，它包含所有的传入迭代参数对象的值（也包括非 promise 值）。
  >   + 如果传入的 promise 中有一个失败（rejected），Promise.all 异步地将失败的那个结果给失败状态的回调函数，而不管其它 promise 是否完成。
  >
  > - `Promise.race()`
  >   + 常见使用场景：把异步操作和定时器放到一起，如果定时器先触发，认为超时，告知用户
  >   + 它接受一个可迭代对象，类似Array。
  >   + 返回一个待定的 Promise 只要给定的迭代中的一个promise解决或拒绝，就采用第一个promise的值作为它的值，从而异步地解析或拒绝（一旦堆栈为空）。
  >   + race 函数返回一个 Promise，它将与第一个传递的 promise 相同的完成方式被完成。它可以是完成（ resolves），也可以是失败（rejects），这要取决于第一个完成的方式是两个中的哪个。
  >   + 如果传的迭代是空的，则返回的 promise 将永远等待。
  >   + 如果迭代包含一个或多个非承诺值和/或已解决/拒绝的承诺，则 Promise.race 将解析为迭代中找到的第一个值。
  >   + 类似于Promise.all(), 区别在于**它有任意一个返回成功后，就算完成，但是进程不会立即停止**

- 15.`async/await` 与 `Promise` 的优缺点有哪些？

  > async/await 是写异步代码的一种方式，以前的方法有回调函数和Promise。
  > async/await 是基于 Promise 实现的，它不能用于普通的回调函数。
  > async/await 与 Promise 一样，是非阻塞的。
  > async/await 使得异步代码看起来像同步代码。
  > await 关键字只能用在 async 定义的函数内。
  > async 函数会隐式地返回一个 Promise，该 Promise 的 resolve 值就是函数 return的值。
  > - async/await 相对于 Promise 的优点
  >   + 1.简洁: 不需要写.then，不需要写匿名函数处理Promise的resolve值，也不需要定义多余的data变量，还避免了嵌套代码。
  >   + 2.错误处理: Promise中， try/catch 不能处理 Promise 中的错误，需要使用 .catch，使用 aync/await 的话，try/catch能处理Promise 中的错误:
  >   + 3.可读性：async/await 编写可以大大地提高可读性。
  >   + 4.错误栈: Promise 链中返回的错误栈不会准确的给出错误发生位置的线索, async/await 中的错误栈会指向错误所在的函数。

- 16.Vue 的子组件中可以修改 props 的值吗？如果修改了会报错吗？
  > 先上张图，看看 Vue.js 作者的看法

  <div style="width:100%;display:flex;flex-direction:column;justify-content:center;text-align:center;">

    <img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/baiduInterview/modifyProps.png" style="width:100%;max-width:600px;margin: 5px auto;">

  </div>

  > 显然，作者都不希望在子组件中去修改父组件中的数据。
  >
  > Vue.js 官网的描述如下：
  >
  > 所有的 prop 都使得其父子 prop 之间形成了一个单向下行绑定：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。这样会防止从子组件意外改变父级组件的状态，从而导致你的应用的数据流向难以理解。
  > 这里有两种常见的试图改变一个 prop 的情形：
  >
  > 这个 prop 用来传递一个初始值；这个子组件接下来希望将其作为一个本地的 prop 数据来使用。在这种情况下，最好定义一个本地的 data 属性并将这个 prop 用作其初始值：
  ```js
    props: ['initialCounter'],
    data: function () {
      return {
        counter: this.initialCounter
      }
    }
  ```
  > 这个 prop 以一种原始的值传入且需要进行转换。在这种情况下，最好使用这个 prop 的值来定义一个计算属性：
  ```js
    props: ['size'],
    computed: {
      normalizedSize: function () {
        return this.size.trim().toLowerCase()
      }
    }
  ```
  > 注意在 JavaScript 中对象和数组是通过引用传入的，所以对于一个数组或对象类型的 prop 来说，在子组件中改变这个对象或数组本身将会影响到父组件的状态。
  > 额外的，每次父级组件发生更新时，子组件中所有的 prop 都将会刷新为最新的值。这意味着你不应该在一个子组件内部改变 prop。如果你这样做了，Vue 会在浏览器的控制台中发出警告。
  > 至于是否报错
  >   - 如果在子组件只是修改 prop 的`值`的话
  >     + 只有 prop 为非引用类型数据，譬如字符串，数字等，才会报错。
  >     + 而对于引用类型的数据，如对象，数组等，不会报错。个人认为其原因可能是只是修改了其内部的值，其指针的指向性并没有发生改变。
  >   - 如果在子组件修改 prop 数组、对象的指针指向
  >     + 会报错
  >
  > <code style="color:red;">
  >   [Vue warn]: Avoid mutating a prop directly since the value will be overwritten whenever the parent component re-renders. Instead, use a data or computed property based on the prop's value.
  > </code>

- 17.手写一下深拷贝的代码吧。

  > MDN 上的`取巧`写法
  ```js
    const deepClone = (obj) => JSON.parse(JSON.stringify(obj));
  ```
  > 这种写法如果出现循环引用的话，`JSON.stringify(obj)` 会抛出异常，而且不能够识别Function，因此这种写法适用于一些比较简单无循环引用、无Function的对象深拷贝
  >
  > 经过琢磨，自己写了一个深拷贝的类，感觉要解决循环引用问题，只用一个方法还是有点困难的，所以通过类里的多个方法和属性协同解决。代码如下：

  ```js
  // 原创代码，只此一家，如有雷同，纯属巧合

    class DeepClone {
      constructor(obj) {
        this.src = obj || {};
        // 要拷贝的对象
        this.hasClonedObj = [];
        // 缓存 已经拷贝过的 object
        this._Circular_reference_tag = '$ref';
        // 循环引用占位符
      }
      reset() {
        // 清空已经拷贝过的 object
        this.hasClonedObj = [];
        return this;
      }
      finishedCloneObj(obj) {
        // 暂存已经拷贝过的 object， 用于判断是否循环引用
        if (this.hasClonedObj.every(e => e !== obj)) {
          this.hasClonedObj.push(obj);
        }
      }
      hasObjClone(obj) {
        // 判断 obj 是否已经拷贝过，即判断是否有循环引用
        let rs = { hasClone: false, index: null };
        this.hasClonedObj.forEach((e, i) => {
          if (obj === e) {
            rs = { hasClone: true, index: i };
          }
        });
        return rs;
      }
      deepClone(src) {
        this.reset();
        // 清空缓存    
        return this.deepCloneCore(src || this.src);
        // 深度拷贝
      }
      cloneAndParseCR(src){
        this.reset();
        // 清空缓存    
        return this.parseCircularReference(this.deepCloneCore(src || this.src));
        // “深”度拷贝 还原循环引用
      }
      parseCircularReference(rsObj) {
        // 解析循环引用，还原占位符
        if (typeof rsObj === 'object') {
          if (Array.isArray(rsObj)) {
            rsObj.forEach(e => this.parseCircularReference(e))
            // 递归深解析循环引用
          } else {
            if (rsObj === null) return null;
            // 如果时 null，直接返回 null
            Object.keys(rsObj).forEach(key => {
              if (rsObj.hasOwnProperty(key)) {
                rsObj[key] = this.parseCircularReference(rsObj[key])
              }
            })
          }
        } else if (typeof rsObj === 'string') {
          if (rsObj.includes(this._Circular_reference_tag)){
            let crObj = this.hasClonedObj[Number(rsObj.match(/[0-9]+/)[0])];
            rsObj = Array.isArray(crObj) ? [...crObj] : {...crObj};
            // 还原占位符， 此处为深度为一的"深"拷贝，本质为浅拷贝
          }
        }
        return rsObj;
      }
      deepCloneCore(src) {
        let target;
        if (typeof src === 'object') {
          let { hasClone, index } = this.hasObjClone(src);
          if (hasClone) {
            // 如果循环引用
            return `${this._Circular_reference_tag}_${index}`
            // 返回占位符与下标组成的字符串
          } else if (src) {
            this.finishedCloneObj(src);
            // 缓存已经拷贝过的对象
          }
          if (Array.isArray(src)) {
            target = [];
            src.forEach((e, i) => target[i] = this.deepCloneCore(e))
            // 递归深度拷贝数组
          } else {
            if (src === null) return null;
            // 如果时 null，直接返回 null
            target = {};
            Object.keys(src).forEach(key => {
              if (src.hasOwnProperty(key)) {
                target[key] = this.deepCloneCore(src[key])
              }
            })
            // 循环递归深度拷贝对象
          } 
        } else {        
          target = src
          // 非 object 类型直接赋值拷贝
        }
        return target
        // 返回拷贝结果
      }
    }
  ```
  > 其实 17题 是由 16题 而来的，面试官提问的顺序极其有逻辑，如果你还不太清楚 16题 和 17题 有啥关系，那么可以`康康`这篇文章[在vue中子组件修改props引发的对js深拷贝和浅拷贝的思考](https://www.cnblogs.com/hutuzhu/p/10119698.html);

感谢你能看到这里！本人能力有限，本文中可能有些纰漏或者不正确之处，还请批评指正。
<br>
以上！