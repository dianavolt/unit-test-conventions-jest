# Snapshots

#### Use snapshots for Styled Components

```javascript
// [styled component in a div]

describe('StyledComponent', () => {
    it('should match snapshot', () => {
        expect(shallow(<StyledComponent/>)).toMatchSnapshot()
    })
})
```

#### Perform shallow render on React components
When possible use [shallow](https://enzymejs.github.io/enzyme/docs/api/shallow.html) render instead of snapshot testing on React components. 
Enzyme's shallow render checks if certain elements exist or if their value is affected by passing configuration prop.

```javascript
// [styled component in a div]

describe('StyledComponent', () => {
    let sut
    let props

    beforeEach(() => {
        props = { searchName: 'Google'}
        sut = render(props)
    })

    it('should match snapshot', () => {
        const name = sut.find('.name')

        expect(name).toBe(props.searchName)
    })
})

