# svelte-philosophies

Based on [react-philosophies](https://github.com/mithi/react-philosophies)

> You have to think about what is the right way, even when you have the right idea of what the building blocks should be, there is huge flexibility in how you decide to put the whole system together. It is a craft... and it has a lot to do with valuing simplicity over complexity. Many people do have a tendency to make things more complicated than they need to be... The more stuff you throw into a system, the more complicated it gets and the more likely it is not going to work properly. - Barbara Liskov

## 🧘 0. Introduction

`react-philosophies` is:

- things I think about when I write `React` code.
- at the back of my mind whenever I review someone else's code or my own
- just guidelines and NOT rigid rules
- a living document and will evolve over time as my experience grows
- mostly techniques which are variations of basic [refactoring](https://en.wikipedia.org/wiki/Code_refactoring) methods, [SOLID](https://en.wikipedia.org/wiki/SOLID) principles, and [extreme programming](https://en.wikipedia.org/wiki/Extreme_programming) ideas...


> As a seasoned developer I have certain quirks, opinions, and common patterns that I fall back on. Having to explain to another person why I am approaching a problem in a particular way is really good for helping me break bad habits and challenge my assumptions, or for providing validation for good problem solving skills. - [Coraline Ada Ehmke](https://where.coraline.codes)

## 🧘 1. The Bare Minimum

### 1.1 Recognize when the computer is smarter than you

1. Statically analyze your code with [`ESLint`](https://eslint.org/). 
2. Enable ["strict"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode) mode. It's 2022. 
8. There is a reason why errors and warnings are displayed in the console.
10. [Prettier](https://prettier.io/) (or an alternative) formats your code for you, giving you consistent formatting every time. You no longer need to think about it!
11. [`Typescript`](https://www.typescriptlang.org/) and frameworks such as [`NextJS`](https://nextjs.org/) make your life so much easier.
12. I highly recommend [Code Climate](https://codeclimate.com/quality/) (or similar) for open-source repositories or if you can afford it. I find that automatically-detected code smells truly motivates me to reduce the technical debts of the application I'm working on!

### 1.2 Code is just a necessary evil

> "The best code is no code at all. Every new line of code you willingly bring into the world is code that has to be debugged, code that has to be read and understood, code that has to be supported." - Jeff Atwood

> "One of my most productive days was throwing away 1000 lines of code." - Eric S. Raymond

See also: [Write Less Code - Rich Harris](https://svelte.dev/blog/write-less-code), [Code is evil - Artem Sapegin](https://github.com/sapegin/washingcode-book/blob/master/manuscript/Code_is_evil.md)

#### 1.2.1 Think first before adding another dependency

Needless to say, the more you add dependencies, the more code you ship to the browser. Ask yourself, are you actually using the features which make a particular library great?


#### 1.2.2 Don't be clever. YAGNI!

> "What could happen with my software in the future? Oh yeah, maybe this and that. Let’s implement all these things since we are working on this part anyway. That way it’s future-proof."

**Y**ou **A**ren't **G**onna **N**eed **I**t! Always implement things when you actually need them, never when you just foresee that you may need them. The less code the better! ([Martin Fowler: YAGNI](https://martinfowler.com/bliki/Yagni.html), [C2 Wiki: You Arent Gonna Need It!](https://wiki.c2.com/?YouArentGonnaNeedIt))

Related section: [2.4 Duplication is far cheaper than the wrong abstraction](#-24-duplication-is-far-cheaper-than-the-wrong-abstraction)

### 1.3 Leave it better than you found it

**1.3.1 Detect code smells and do something about them if you need to**. 

If you recognize that something is wrong, fix it right then and there. But if it's not that easy to fix or you don't have time to fix it at that moment, at least add a comment (`FIXME` or `TODO`) with a concise explanation of the identified problem. Make sure everybody knows it is broken. It shows others that you care and that they should also do the same when they encounter those kinds of things.

<details>
    <summary><strong>🙈 View examples of easy-to-catch code smells</strong></summary>

<br/>

- ❌ Methods or functions defined with a large number of arguments
- ❌ Boolean logic that may be hard to understand
- ❌ Excessive lines of code within a single file
- ❌ Duplicate code which is syntactically identical (but may be formatted differently)
- ❌ Functions or methods that may be hard to understand
- ❌ Classes / Components defined with a large number of functions or methods
- ❌ Excessive lines of code within a single function or method
- ❌ Functions or methods with a large number of return statements
- ❌ Duplicate code which is not identical but shares the same structure (e.g. variable names may differ)


Keep in mind that code smells don't necessarily mean that code should be changed. A code smell just informs you that you might be able to think of a better way to implement the same functionality.

**1.3.2 Merciless Refactoring. Simple is better than complex.**

> Is the CL more complex than it should be? Check this at every level of the CL—are individual lines too complex? Are functions too complex? Are classes too complex? “Too complex” usually means “can’t be understood quickly by code readers.” It can also mean “developers are likely to introduce bugs when they try to call or modify this code.”- [Google Engineering Practices: What to look for in a code review](https://google.github.io/eng-practices/review/reviewer/looking-for.html)


**💁‍♀️ TIP: Prefer chained higher-order functions over loops**

If there is no discernable performance difference and if possible, replace traditional loops with chained higher-order functions (`map`, `filter`, `find`, `findIndex`, `some`, etc) [Stackoverflow: What is the advantage of using a function over loops?](https://stackoverflow.com/questions/34402198/what-is-the-advantage-of-using-a-function-over-loops)


### 1.4 You can do better


**💁‍♀️ TIP: Think about how your component will be used before coding it**

[Writing APIs is hard](http://sweng.the-davies.net/Home/rustys-api-design-manifesto). [`README Driven Development`](https://tom.preston-werner.com/2010/08/23/readme-driven-development.html) is one useful technique to help design better APIs.  I'm not saying we should [RDD](https://rathes.me/blog/en/readme-driven-development/) religiously, just saying that the idea behind it is great. I find that when I first write the API (how the component will be used) before implementing it, this usually creates a better designed component than when I don't.

## 🧘 2. Design for happiness

> "Any fool can write code that a computer can understand. Good programmers write code that humans can understand." - Martin Fowler

> "The ratio of time spent reading versus writing is well over 10 to 1. We are constantly reading old code as part of the effort to write new code. So if you want to go fast, if you want to get done quickly, if you want your code to be easy to write, make it easy to read." ― Robert C. Martin [(Not saying I agree with his political views)](https://www.getrevue.co/profile/tech-bullshit/issues/tech-bullshit-explained-uncle-bob-830918)

**TL;DR**

1. 💖 Avoid state management complexity by removing redundant states
2. 💖 Pass the banana, not the gorilla holding the banana and the entire jungle (prefer passing primitives as props)
3. 💖 Keep your components small and simple - the single responsibility principle!
4. 💖 Duplication is far cheaper than the wrong abstraction (avoid premature / inappropriate generalization)
5. Avoid prop drilling by using composition ([Michael Jackson](https://www.youtube.com/watch?v=3XaXKiXtNjw)). `Context` is not the solution for every state sharing problem
6. Split giant `useEffect`s to smaller independent ones ([KCD: Myths about useEffect](https://epicreact.dev/myths-about-useeffect))
7. Extract logic to hooks and helper functions
8. Prefer having mostly primitives as dependencies to `useCallback`, `useMemo`, and `useEffect`
9. Do not put too many dependencies in `useCallback`, `useMemo`, and `useEffect`
10. For simplicity, instead of having many `useState`s, consider using `useReducer` if some values of your state rely on other values of your state and previous state
11. `Context` does not have to be global to your whole app. Put `Context` as low as possible in your component tree. Do this the same way you put variables, comments, states (and code in general) as close as possible to where they're relevant / being used.

### 💖 2.1 Avoid state management complexity by removing redundant states

When you have redundant states, some states may fall out of sync; you may forget to update them given a complex sequence of interactions.
Aside from avoiding synchronization bugs, you'd notice that it's also easier to reason about and require less code.
See also: [KCD: Don't Sync State. Derive It!](https://kentcdodds.com/blog/dont-sync-state-derive-it), [Tic-Tac-Toe](https://epic-react-exercises.vercel.app/react/hooks/1)

##### 🙈 Example 1

<details>
    <summary><strong> 📝🖊️ View the business requirement / problem statement </strong></summary>


---

You are tasked to display properties of a right triangle
- the lengths of each of the three sides
- the perimeter
- the area

The triangle is an object with two numbers `{a: number, b: number}` that should be fetched from an API. 
The two numbers represent the two shorter sides of a right triangle.

---

</details>

<details>
 <summary> ❌ View not-so-good Solution </summary>

```tsx
const TriangleInfo = () => {
  const [triangleInfo, setTriangleInfo] = useState<{a: number, b: number} | null>(null)
  const [hypotenuse, setHypotenuse] = useState<number | null>(null)
  const [perimeter, setPerimeter] = useState<number | null>(null)
  const [areas, setArea] = useState<number | null>(null)

  useEffect(() => {
    fetchTriangle().then(t => setTriangleInfo(t))
  }, [])

  useEffect(() => {
    if(!triangleInfo) {
      return
    }
    
    const { a, b } = triangleInfo
    const h = computeHypotenuse(a, b)
    setHypotenuse(h)
    const newArea = computeArea(a, b)
    setArea(newArea)
    const p = computePerimeter(a, b, h)
    setPerimeter(p)

  }, [triangleInfo])

  if (!triangleInfo) {
    return null
  }

  /*** show info here ****/
}
````

</details>

<details>
  <summary> ✅ View "better" solution </summary>

```tsx
const TriangleInfo = () => {
  const [triangleInfo, setTriangleInfo] = useState<{
    a: number;
    b: number;
  } | null>(null)

  useEffect(() => {
    fetchTriangle().then((r) => setTriangleInfo(r))
  }, []);

  if (!triangleInfo) {
    return
  }

  const { a, b } = triangeInfo
  const area = computeArea(a, b)
  const hypotenuse = computeHypotenuse(a, b)
  const perimeter = computePerimeter(a, b, hypotenuse)
 
  /*** show info here ****/
};
```

</details> 
  
##### 🙈 Example 2

<details>
    <summary><strong> 📝🖊️ View the business requirement / problem statement </strong></summary>


---

Suppose you are assigned to design a component which:

1. Fetches a list of unique points from an API
2. Includes a button to either sort by `x` or `y` (ascending order)
3. Includes a button to change the `maxDistance` (increase by `10` each time, initial value should be `100`)
4. Only displays the points that are NOT farther than the current `maxDistance` from the origin `(0, 0)`
5. Assume that the list only has 100 items (meaning you don't need to worry about optimization). If you're working with really large numbers of items, you can memoize some computations with `useMemo`.

---

</details>

<details>
  <summary> ❌ View a not-so-good Solution </summary>
  
```tsx
type SortBy = 'x' | 'y'
const toggle = (current: SortBy): SortBy => current === 'x' ? : 'y' : 'x'

const Points = () => {
  const [points, setPoints] = useState<{x: number, y: number}[]>([])
  const [filteredPoints, setFilteredPoints] = useState<{x: number, y: number}[]>([])
  const [sortedPoints, setSortedPoints] = useState<{x: number, y: number}[]>([])
  const [maxDistance, setMaxDistance] = useState<number>(100)
  const [sortBy, setSortBy] = useState<SortBy>('x')
  
  useEffect(() => {
    fetchPoints().then(r => setPoints(r))
  }, [])
  
  useEffect(() => {
    const sorted = sortPoints(points, sortBy)
    setSortedPoints(sorted)
  }, [sortBy, points])

  useEffect(() => {
    const filtered = sortedPoints.filter(p => getDistance(p.x, p.y) < maxDistance)
    setFilteredPoints(filtered)
  }, [sortedPoints, maxDistance])

  const otherSortBy = toggle(sortBy)
  const pointToDisplay = filteredPoints.map(
    p => <li key={`${p.x}|{p.y}`}>({p.x}, {p.y})</li>
  )

  return (
    <>
      <button onClick={() => setSortBy(otherSortBy)}>
        Sort by: {otherSortBy}
      <button>
      <button onClick={() => setMaxDistance(maxDistance + 10)}>
        Increase max distance
      <button>
      Showing only points that are less than {maxDistance} units away from origin (0, 0)
      Currently sorted by: '{sortBy}' (ascending)
      <ol>{pointToDisplay}</ol>
    </>
  )
}

````
</details>

<details>
  <summary> ✅ View a "better" Solution </summary>

```tsx

// NOTE: You can also use useReducer instead
type SortBy = 'x' | 'y'
const toggle = (current: SortBy): SortBy => current === 'x' ? : 'y' : 'x'

const Points = () => {
  const [points, setPoints] = useState<{x: number, y: number}[]>([])
  const [maxDistance, setMaxDistance] = useState<number>(100)
  const [sortBy, setSortBy] = useState<SortBy>('x')

  useEffect(() => {
    fetchPoints().then(r => setPoints(r))
  }, [])
  

  const otherSortBy = toggle(sortBy)
  const filtedPoints = points.filter(p => getDistance(p.x, p.y) < maxDistance)
  const pointToDisplay = sortPoints(filteredPoints, sortBy).map(
    p => <li key={`${p.x}|{p.y}`}>({p.x}, {p.y})</li>
  )

  return (
    <>
      <button onClick={() => setSortBy(otherSortBy)}>
        Sort by: {otherSortBy} <button>
      <button onClick={() => setMaxDistance(maxDistance + 10)}>
        Increase max distance
      <button>
      Showing only points that are less than {maxDistance} units away from origin (0, 0)
      Currently sorted by: '{sortBy}' (ascending)
      <ol>{pointToDisplay}</ol>
    </>
  )
}
````

</details>

### 💖 2.2 Pass the banana, not the gorilla holding the banana and the entire jungle

> You wanted a banana but what you got was a gorilla holding the banana and the entire jungle. - Joe Armstrong

To avoid falling into this trap, it's a good idea to pass mostly primitives (`boolean`, `string`, `number`, etc) types as props. (Passing primitives is also a good idea if you want to use `React.memo` for optimization)

> A component should just know enough to do its job and nothing more. As much as possible, components should be able to collaborate with others without knowing what they are and what they do.

When we do this, the components will be more loosely coupled, the degree of dependency between two components will be lower. Loose coupling makes it easier to change, replace, or remove components without affecting other components. [stackoverflow:2832017](https://stackoverflow.com/questions/2832017/what-is-the-difference-between-loose-coupling-and-tight-coupling-in-the-object-o)

##### 🙈 Example

<details>
    <summary><strong> 📝🖊️ View the business requirement / problem statement </strong></summary>


---

Create a `MemberCard` component that displays two components: `Summary` and `SeeMore`.
The `MemberCard` takes in the prop `id` . The `MemberCard` consumes the hook `useMember` which takes in an `id` and returns the corresponding `Member` information.

```ts
type Member = {
  id: string
  firstName: string
  lastName: string
  title: string
  imgUrl: string
  webUrl: string
  age: number
  bio: string
  /****** 100 more fields ******/
}
```

The `SeeMore` component should display the `age` and `bio` of the `member`.
Include a button to toggle between showing and hiding the `age` and `bio` of the `member`.

The `Summary` component displays the picture of the `member`. 
It also displays his `title`, `firstName` and `lastName` (e.g. `Mr. Vincenzo Cassano`). 
Clicking the `member`'s name should take you to the `member`'s personal site.
The `Summary` component may also have other functionalities. 
(Example, whenever this component is clicked...
the font, size of the image, and background color are randomly changed...
for brevity let's call this "the random styling feature")

---

</details>

<details>
  <summary>❌ View a not-so-good solution</summary>
  
```tsx

const Summary = ({ member } : { member: Member }) => {
  /*** include "the random styling feature" ***/
  return (
    <>
      <img src={member.imgUrl} />
      <a href={member.webUrl} >
        {member.title}. {member.firstName} {member.lastName}
      </a>
    </>
  )
}

const SeeMore = ({ member }: { member: Member }) => {
  const [seeMore, setSeeMore] = useState<boolean>(false)
  return (
    <>
      <button onClick={() => setSeeMore(!seeMore)}>
        See {seeMore ? "less" : "more"}
      </button>
      {seeMore && <>AGE: {member.age} | BIO: {member.bio}</>}
    </>
  )
}

const MemberCard = ({ id }: { id: string })) => {
  const member = useMember(id)
  return <><Summary member={member} /><SeeMore member={member} /></>
}

````

</details>


<details>
  <summary>✅ View a "better" solution</summary>

```tsx

const Summary = ({ imgUrl, webUrl, header }: { imgUrl: string, webUrl: string, header: string }) => {
  /*** include "the random styling feature" ***/
  return (
    <>
      <img src={imgUrl} />
      <a href={webUrl}>{header}</a>
    </>
  )
}

const SeeMore = ({ componentToShow }: { componentToShow: ReactNode }) => {
  const [seeMore, setSeeMore] = useState<boolean>(false)
  return (
    <>
      <button onClick={() => setSeeMore(!seeMore)}>
        See {seeMore ? "less" : "more"}
      </button>
      {seeMore && <>{componentToShow}</>}
    </>
  )
}


const MemberCard = ({ id }: { id: string }) => {
  const { title, firstName, lastName, webUrl, imgUrl, age, bio } = useMember(id)
  const header = `${title}. ${firstName} ${lastName}`
  return (
    <>
      <Summary {...{ imgUrl, webUrl, header }} />
      <SeeMore componentToShow={<>AGE: {age} | BIO: {bio}</>} />
    </>
  )
}
````

</details>
    
Notice that in the `✅  "better" solution"`, `SeeMore` and `Summary` are components that can be used not just by `Member`. It can be used perhaps by other objects such as `CurrentUser`, `Pet`, `Post`... anything that needs those specific functionality.

### 💖 2.3 Keep your components small and simple

**What is the single responsibility principle?**

> A component should have one and **only one** job. It should do the smallest possible useful thing. It only has responsibilities that fulfill its purpose.

A component with various responsibilities is difficult to reuse. If you want to reuse some but not all of its behavior, it's almost always impossible to just get what you need. It is also likely to be entangled with other code. Components that do one thing which isolate that thing from the rest of your application allows change without consequence and reuse without duplication.

**How to know if your component has a single responsibility?**

> Try to describe that component in one sentence. If it is only responsible for one thing then it should be simple to describe. If it uses the word ‘and’ or ‘or’ then it is likely that your component fails this test.

Inspect the component's state, the props and hooks it consumes, as well as variables and methods declared inside the component (there shouldn't be too many). Ask yourself: Do these things actually work together to fulfill the component's purpose? If some of them don't, consider moving those somewhere else or breaking down your big component into smaller ones.

(The paragraphs above are based on my 2015 article: [Three things I learned from Sandi Metz’s book as a non-Ruby programmer](https://medium.com/@mithi/review-sandi-metz-s-poodr-ch-1-4-wip-d4daac417665))

##### 🙈 Example

<details>
    <summary><strong> 📝🖊️ View the business requirement / problem statement </strong></summary>


---

The requirement is to display special kinds of buttons you can click to shop for items of a specific category. For example, the user can select bags, chairs, and food.

- Each button opens a modal you can use to select and "save" items
- If the user has "saved" selected items in a specific category, that category said to be "booked"
- If it is booked, the button will have a checkmark
- You should be able to edit your booking (add or delete items) even if that category is booked
- If the user is hovering the button it should also display `WavingHand` component
- A button should also be disabled when no items for that specific category is available
- When a user hovers a disabled button, a tooltip should show "Not Available"
- If the category has no items available, the button's background should be `grey`
- If the category is booked, the button's background should be `green`
- If the category has available items and is not booked, the button's background should be `red`
- For each category, its corresponding button has a unique label and icon

---

</details>
   
<details>
    <summary>❌ View a not-so-good solution</summary>

```tsx
type ShopCategoryTileProps = {
  isBooked: boolean
  icon: ReactNode
  label: string
  componentInsideModal?: ReactNode
  items?: {name: string, quantity: number}[]
}

const ShopCategoryTile = ({
  icon,
  label,
  items
  componentInsideModal,
}: ShopCategoryTileProps ) => {
  const [openDialog, setOpenDialog] = useState(false)
  const [hover, setHover] = useState(false)
  const disabled = !items || items.length  === 0
  return (
    <>
      <Tooltip title="Not Available" show={disabled}>
        <StyledButton
          className={disabled ? "grey" : isBooked ? "green" : "red" }
          disabled={disabled}
          onClick={() => disabled ? null : setOpenDialog(true) }
          onMouseEnter={() => disabled ? null : setHover(true)}
          onMouseLeave={() => disabled ? null : setHover(false)}
        >
          {icon}
          <StyledLabel>{label}<StyledLabel/>
          {!disabled && isBooked && <FaCheckCircle/>}
          {!disabled && hover && <WavingHand />}
        </StyledButton>
      </Tooltip>
      {componentInsideModal &&
        <Dialog open={openDialog} onClose={() => setOpenDialog(false)}>
          {componentInsideModal}
        </Dialog>
      }
    </>
  )
}
```

</details>
          
<details>
    <summary>✅ View a "better" solution</summary>

```tsx
// split into two smaller components!

const DisabledShopCategoryTile = ({ icon, label }: { icon: ReactNode, label: string }) => {
  return (
    <Tooltip title="Not available">
      <StyledButton disabled={true} className="grey">
        {icon}
        <StyledLabel>{label}<StyledLabel/>
      </Button>
    </Tooltip>
  )
}

type ShopCategoryTileProps = {
  icon: ReactNode
  label: string
  isBooked: boolean
  componentInsideModal: ReactNode
}

const ShopCategoryTile = ({
  icon,
  label,
  isBooked,
  componentInsideModal,
}: ShopCategoryTileProps ) => {
  const [openDialog, setOpenDialog] = useState(false)
  const [hover, setHover] = useState(false)

  return (
    <>
      <StyledButton
        disabled={false}
        className={isBooked ? "green" : "red"}
        onClick={() => setOpenDialog(true) }
        onMouseEnter={() => setHover(true)}
        onMouseLeave={() => setHover(false)}
      >
        {icon}
        <StyledLabel>{label}<StyledLabel/>
        {isBooked && <FaCheckCircle/>}
        {hover && <WavingHand />}
      </StyledButton>
      {openDialog &&
        <Dialog onClose={() => setOpenDialog(false)}>
          {componentInsideModal}
        </Dialog>
      }}
    </>
  )
}
```

</details>

Note: The example above is a simplified version of a component that I've actually seen in production

<details>
    <summary>❌ View a not-so-good solution</summary>

```tsx
const ShopCategoryTile = ({
  item,
  offers,
}: {
  item: ItemMap;
  offers?: Offer;
}) => {
  const dispatch = useDispatch();
  const location = useLocation();
  const history = useHistory();
  const { items } = useContext(OrderingFormContext)
  const [openDialog, setOpenDialog] = useState(false)
  const [hover, setHover] = useState(false)
  const isBooked =
    !item.disabled && !!items?.some((a: Item) => a.itemGroup === item.group)
  const isDisabled = item.disabled || !offers
  const RenderComponent = item.component

  useEffect(() => {
    if (openDialog && !location.pathname.includes("item")) {
      setOpenDialog(false)
    }
  }, [location.pathname]);
  const handleClose = useCallback(() => {
    setOpenDialog(false)
    history.goBack()
  }, [])

  return (
    <GridStyled
      xs={6}
      sm={3}
      md={2}
      item
      booked={isBooked}
      disabled={isDisabled}
    >
      <Tooltip
        title="Not available"
        placement="top"
        disableFocusListener={!isDisabled}
        disableHoverListener={!isDisabled}
        disableTouchListener={!isDisabled}
      >
        <PaperStyled
          disabled={isDisabled}
          elevation={isDisabled ? 0 : hover ? 6 : 2}
        >
          <Wrapper
            onClick={() => {
              if (isDisabled) {
                return;
              }
              dispatch(push(ORDER__PATH));
              setOpenDialog(true);
            }}
            disabled={isDisabled}
            onMouseEnter={() => !isDisabled && setHover(true)}
            onMouseLeave={() => !isDisabled && setHover(false)}
          >
            {item.icon}
            <Typography variant="button">{item.label}</Typography>
            <CheckIconWrapper>
              {isBooked && <FaCheckCircle size="26" />}
            </CheckIconWrapper>
          </Wrapper>
        </PaperStyled>
      </Tooltip>
      <Dialog fullScreen open={openDialog} onClose={handleClose}>
        {RenderComponent && (
          <RenderComponent item={item} offer={offers} onClose={handleClose} />
        )}
      </Dialog>
    </GridStyled>
  )
}
```

</details>

> Not only should a component have a single responsibility, it should also have a clear spot on the spectrum of abstraction. On one end, we have generic building blocks like `<Button>`, `<Heading>`, `<Modal>`. On the other end, we have one-off templates like `<Homepage>` and `<ContactForm>`. Every component should have a clear spot on this spectrum. A `<Button>` component shoudn't have a _user_ prop, since users are a higher-abstract concept and `Button` is a low-abstract component.


### 💖 2.4 Duplication is far cheaper than the wrong abstraction

Avoid premature / inappropriate generalization. If your implementation for a simple feature requires a huge overhead, consider other options.
I highly recommend reading [Sandi Metz: The Wrong Abstraction](https://sandimetz.com/blog/2016/1/20/the-wrong-abstraction).

> A particular type of complexity is over-engineering, where developers have made the code more generic than it needs to be, or added functionality that isn’t presently needed by the system. Encourage developers to solve the problem they know needs to be solved now, not the problem that the developer speculates might need to be solved in the future. The future problem should be solved once it arrives and you can see its actual shape and requirements in the physical universe. - [Google Engineering Practices: What to look for in a code review](https://google.github.io/eng-practices/review/reviewer/looking-for.html)

See also: [KCD: AHA Programming](https://kentcdodds.com/blog/aha-programming), [C2 Wiki: Contrived Interfaces](https://wiki.c2.com/?ContrivedInterfaces)/[The Expensive Setup Smell](https://wiki.c2.com/?ExpensiveSetUpSmell)/[Premature Generalization](https://wiki.c2.com/?PrematureGeneralization)


6. Putting your state as close as possible to where it's being used will not only make your code so much easier to read but it would also make your app faster (state colocation)
7. `Context` should be logically separated, do not add too many values in one context provider. If any of the values of your context changes, all components consuming that context also rerenders even if those components don't use the specific value that was actually changed.


> Premature optimization is the root of all evil - Tony Hoare
        

(Note, the above is taken from his response to my email... I really appreciate that he took the time to share his ideas 🙂)
