# Test Hierarchy

#### Group test cases in 'describe' blocks
This will provide a clean hierarchy of cases.
Nested 'describe' description should start with 'when'.
'it' descriptions should start with 'should'

```javascript
describe('ComponentName', () => {
    // ...
    describe('when case X...', () => {
        it('should do ...', () => {
            // response 1
        })
        it('should also do ...', () => {
            // reponse 2
        })
    })

    describe('when case Y...', () => {
        describe('when type is A', () => {
            it('should do...', () => {
                // reponse 3
            })

            it('should also do...', () => {
                // reponse 4
            })
        })

        describe('when type is B', () => {
            it('should do...', () => {
                // reponse 5
            })

            it('should also do...', () => {
                // reponse 6
            })
        })
    })
})
