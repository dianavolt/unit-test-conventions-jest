# Variables

#### Initialize variables in 'beforeEach'
This will eliminate possible mutations or variable changes in nested 
'describe' or 'it' blocks

```javascript
describe('ComponentName', () => {
    let sut
    let props
    let mockData

    beforeEach(() => {
        props = {
            text: 'Text',
            onChange: jest.fn()
        }
        mockData = {
            goTo: jest.fn()
        }
    }
})
```

#### Group variable declarations
Setting [Spies](https://jestjs.io/docs/jest-object#jestspyonobject-methodname) and rendering in several 'beforeEach' blocks to keep it readable

```javascript
describe('ComponentName', () => {
    let sut
    let props
    let mockData

    beforeEach(() => {
        props = {
            text: 'Text',
            onChange: jest.fn()
        }
        mockData = {
            goTo: jest.fn()
        }
    }

    beforeEach(() => {
        jest.spyOn(Obj, 'property').mockReturnValue(mockData)
        jest.spyOn(Obj2, 'property2').mockReturnValue(mockData)
    })

    beforeEach(() => {
        sut = mount(<Component {...props}/>)
    })
})
```

mockResponse example:
```javascript
describe('ComponentName', () => {
    let sut
    let props
    let mockData
    let mockResponse

    beforeEach(() => {
        props = {
            text: 'Text',
            onChange: jest.fn()
        }
        mockData = {
            goTo: jest.fn()
        }
        mockResponse = {
            code: 404
        }
    }

    beforeEach(() => {
        jest.spyOn(Obj, 'property').mockReturnValue(mockData)
        jest.spyOn(Obj2, 'get').mockReturnValue(mockResponse)

        sut = mount(<Component {...props}/>)
    })
})
```


