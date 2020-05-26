##  Hook ( React 16.8 的新增特性 )

### State Hook (useState)

    类似 class 组件的 this.setState,  但是它不会把新的 state 和旧的 state 进行合并。
    useState 唯一的参数就是初始 state，useState 会返回一对值：当前状态和一个让你更新它的函数。
    
    function ExampleWithManyStates() {
    // 声明多个 state 变量！
    const [age, setAge] = useState(42);
    const [fruit, setFruit] = useState('banana');
    const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
    // ...
    } 

### Effect Hook (useEffect)

    跟 class 组件中的 componentDidMount、componentDidUpdate 和 componentWillUnmount 具有相同的用途，只不过被合并成了一个 API
    默认情况下，它在第一次渲染之后和每次更新之后都会执行
    
    useEffect(() => {
            event.on('header.resize', updateHeight)
            return () => {
                event.off('header.resize', updateHeight)
            }
    }, [event, updateHeight]) // 仅在 updateHeight, event 发生变化时，重新订阅

### Callback Hook (useCallback)
        
    useCallback 缓存函数 仅在某个依赖项改变时才会更新
    useMemo     缓存值 仅会在某个依赖项改变时才重新计算返回值        
    useCallback(fn, deps) 相当于 useMemo(() => fn, deps)。
    
    const handleFilter = useCallback((e, state) => {
        setFilterState(state)
    }, [])
    
    const titleList = useMemo(() => {
        const ret = []
        Object.keys(MAIN_TYPE).forEach(key => {
            ret.push({
                key,
                title: MAIN_TYPE[key]
            })
        })
        return ret
    }, [])

### Ref Hook (useRef)
    
    与react ref类似，使用更加简洁    
    function TextInputWithFocusButton() {
      const inputEl = useRef(null);
      const onButtonClick = () => {
        // `current` 指向已挂载到 DOM 上的文本输入元素
        inputEl.current.focus();
      };
      return (
        <>
          <input ref={inputEl} type="text" />
          <button onClick={onButtonClick}>Focus the input</button>
        </>
      );
    }

### useImperativeHandle

    useImperativeHandle 可以让你在使用 ref 时自定义暴露给父组件的实例值。
    在大多数情况下，应当避免使用 ref 这样的命令式代码。
    useImperativeHandle 应当与 forwardRef 一起使用
    
    function FancyInput(props, ref) {
      const inputRef = useRef();
      useImperativeHandle(ref, () => ({
        focus: () => {
          inputRef.current.focus();
        }
      }));
      return <input ref={inputRef} ... />;
    }
    FancyInput = forwardRef(FancyInput);

### [hooks规则](https://react.docschina.org/docs/hooks-rules.html)

### React.memo(React v16.6.0新出的包装函数) 

    React.memo()是一个高阶函数，它与 React.PureComponent类似，
    但是一个函数组件而非一个类
    
    React.memo()可接受2个参数，第一个参数为纯函数的组件，
    第二个参数用于对比props控制是否刷新，与shouldComponentUpdate()功能类似
    






