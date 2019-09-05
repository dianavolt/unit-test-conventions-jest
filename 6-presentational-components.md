# Presentational Components

#### Lodash ['noop'](https://lodash.com/docs/4.17.15#noop)
'noop' is an alternative to arrow functions `() => {}` when testing Presentational components.

```javascript
describe('ComponentName', () => {
    let sut
    let props

    beforeEach(() => {
        props = {
            handleSubmit: noop,
            errors: { post: 'test post' }
        }

        sut = render({ ...props, errors })
    })

    it('should match snapshot', () => {
        expect(sut).toMatchSnapshot()
    })
})
