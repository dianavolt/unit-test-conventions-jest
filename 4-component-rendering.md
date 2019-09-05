# Component Rendering

#### Extract component rendering to a function
Simplifies the test and prevents repetition

```javascript
const render = (context, props) => mount(
    <Context.Provide value={context}>
        <Component {...props} />
    </Context.Provide>
)

describe('ComponentName', () => {
    let sut
    let context
    let props

    beforeEach(() => {
        context = {
            goTo: jest.fn(),
            goBack: jest.fn()
        }
        props = {
            prop: 'test',
            doThis: jest.fn()
        }
        sut = render(context, props)
    })

    it('should ...', () => {
        // ...
    })

    // for override test cases
    it('should ...', () => {
        sut = render(context, {...props, override: 'value'})
    })
})
```
