# Style Guildelines

#### Declare testing variables at the top of the testing function
```javascript
describe('ComponentName', () => {
    let sut // system under test -- test object
    let props
    let mockData
    //
})
```

#### Add spaces between blocks for reability
```javascript
describe('ComponentName', () => {
    let sut
    let props
    let mockData
    // space
    beforeEach(() => {

    })
    // space
    it('should...', () => {

    })
    // space
    it('should...', () => {
        
    })
})
```

