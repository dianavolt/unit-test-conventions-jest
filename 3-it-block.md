# it

#### Simplifying the 'it' block
Include 'beforeEach' to share values if 'describe' contains several 'it' blocks. Rendering and setting 'spies' can be moved into 'beforeEach' even if describe constains one 'it' but makes the case more readable.

Example:
```javascript
describe('ComponentName', () => {
    describe('when [some condition]', () => {
        it('should [do something]', () => {
            jest.spyOn(api, 'get').mockResolvedValue({text: 'Text'})

            sut = render({...props, overrideProperty: 1})

            sut.props().onSubmit()

            expect(mockUseDeliverData.deliverMethod).toHaveBeenCalled()
        })
    })
})
```

WRONG:
```javascript
describe('ComponentName', () => {
    describe('when [some condition]', () => {
        it('should [do something]', () => {
            const mockData = {
                prop1: 'prop1'
            }

            const mockResponse = {
                prop1: 'prop1'
            }

            jest.spyOn(service, 'getData').mockReturnedValue(mockData)
            jest.spyOn(api, 'get').mockResolvedValue(mockResponse)
            jest.spyOn(utils, 'get').mockResolvedValue({text: 'Text'})
            sut = mount(
                <Context.Provide>
                    <Component {...props, overrideProps: 1} />
                </Context.Provide>
            )

            sut.props().onSubmit()

            expect(api.get).toHaveBeenCalled()
        })
    })
})
```

RIGHT:
```javascript
describe('ComponentName', () => {
    describe('when [some condition]', () => {
        let mockData
        let mockResponse
        let mockUtils

        beforeEach(() => {
            mockData = {
                prop1: 'prop1'
            }

            mockResponse = {
                prop1: 'prop1'
            }

            mockUtils = {
                prop1: 'prop1'
            }
        })


        jest.spyOn(service, 'getData').mockReturnedValue(mockData)
        jest.spyOn(api, 'get').mockResolvedValue(mockResponse)
        jest.spyOn(utils, 'get').mockResolvedValue({text: 'Text'})

        sut = render({...props, overrideProps: 1})

        it('should [do something]', () => {
            sut.props().onSubmit()

            expect(api.get).toHaveBeenCalled()
        })
    })
})
```

#### Use only one 'expect' per 'it'
```javascript
import testFunction from '../testFunction'
import emailFunc from '../emailFunc'

jest.mock('../emailFunc')

describe('testFunction', () => {
    let spyConsole
    let wrongArg
    let correctArg

    beforeEach(() => {
        wrongArg = 'wrong arg'
        correctArg = 'correct arg'
        spyConsole = jest.spyOn(console, 'error')
    })

    // WRONG
    it('should invoke emailFunc() and return false', () => {
        const result = testFunction(wrongArg)

        expect(emailFunc).toHaveBeenCalled()
        expect(result).toBeFalse()
    })

    // CORRECT
    it('should invoke emailFunc()', () => {
        testFunction(correctArg)

        expect(emailFunc).toHaveBeenCalled()
    })

    it('should invoke emailFunc() and return false', () => {
        const result = testFunction(wrongArg)

        expect(result).toBeFalse()
    })
})
```
