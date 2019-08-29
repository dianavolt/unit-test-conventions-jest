# Mocks

#### Do not use empty string, null, or undefined in mock variables
This will help to avoid false positive effects.

```javascript
describe('ComponentName', () => {
    let sut
    let props

    beforeEach(() => {
        props = {
            handleSubmit: noop,
            // DO NOT initialize post with an emptry string
            errors: { post: 'test post' }
        }

        sut = render({ ...props, errors })
    })
})
