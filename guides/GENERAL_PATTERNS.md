# General Patterns

## Avoid conflating view layer logic with styling

### Don't ⛔️

This is a common pattern in MaterialUI and should be avoided.

```typescript
<div>
  <Hidden mdUp>/*Some component*/</Hidden>
  <Hidden mdDown>/* Some component*/</Hidden>
</div>
```

### Do ✅

This pattern uses TailwindCSS and maintains better separation between the view
and its styling

```typescript
<div>
  <div className="block md:hidden">// Some component</div>
  <div className="hidden md:flex">// Some component</div>
</div>
```

## Organize component structures consistently

### Don't ⛔️

This is really hard to read.

```typescript
const Component = () => {
  const classes = useStyles()
  const [someState, setSomeState] = useState("")
  const foo = useSelector(s => s.foo)
  const className="p-4 flex"
  const history = useHistory()
  const dispatch = useDispatch()
  const handleOnClick = () => {
    dispatch(doSomething())
  }

  return (
    // Some views
  )
}
```

### Do ✅

Consistent organization makes it easier for other developers to understand the
code.

```typescript
// Constants
const CLASS_NAME="p-4 flex"

const Component = () => {
  // Hooks
  const classes = useStyles()
  const foo = useSelector(s => s.foo)
  const history = useHistory()
  const dispatch = useDispatch()

  // Local State
  const [someState, setSomeState] = useState("")

  // Handlers
  const handleOnClick = () => {
    dispatch(doSomething())
  }

  return (
    // Some views
  )
}
```

## Avoid inline handlers

### Don't ⛔️

```typescript
<button onClick={e => {
  if (foo) {
    doSomething(e.currentTarget)
  }
}}>
  Do Something
</button>
```

### Do ✅

```typescript
const Component = () => {
  const handleOnClickDoSomething = e => {
    if (foo) {
      doSomething(e.currentTarget)
    }
  }

  return (
    <button onClick={handleOnClickDoSomething}>
      Do Something
    </button>
  )
}
```

## Use consistent structure for function component definition and props

### Don't ⛔️

This is a bit hard to process.

```typescript
type Props = {
  foo: number
  bar: string
}

function Component(props: Props) {
  const { foo, bar } = props

  // ...
}
```

### Do ✅

This is more readable and straightforward.

```typescript
interface ComponentProps {
  foo: number
  bar: string
}

const Component: FC<ComponentProps> = ({ foo, bar }) => {
  // ...
}
```

## Use arrow functions

For consistency and readability.

## Use bare html wherever possible

### Don't ⛔️

This abstraction isn't too helpful and provides an unnecessary layer of
indirection.

```typescript
<Typography variant="h6">
  Some text
</Typography>
```

### Do ✅

This is straightforward and clear.

```typescript
<h6>
  Some text
</h6>
```

## Only comment when absolutely necessary

Comments tend to make code less readable. If your code is not understandable
without comments, it may need to be refactored.

Comments should only be added when something _really_ weird is happening in the
code, and you can't avoid it. For example, something is broken in React itself,
and you need to work around it. The code could be confusing for future readers,
so you add a comment clarifying why something weird is happening.

If you think you need a comment, first ask:

Could I refactor this code to avoid adding a comment?

Could this comment instead go in the commit message?

Could I instead just add a name? For example:

### Don't ⛔️

```typescript
// Check if the user is authenticated, if they are currently editing, and
whether the page is loading, before allowing the user to do something
if (isAuthenticated && isAdmin && !loading) {
  doSomething()
}
```

### Do ✅

```typescript
const canUserEdit = isAuthenticated && isAdmin && !loading

if (canUserEdit) {
  doSomething()
}
```
