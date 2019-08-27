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
