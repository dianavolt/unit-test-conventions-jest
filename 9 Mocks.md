# Mocks

#### Manual mocks for hooks and services
[Manual mocks](https://jestjs.io/docs/manual-mocks) can export a function that can be used to mock returned value for shared hooks or services.
Mocks can be stored in separate file with the same filename as the component name in the __mocks__ folder

```javascript
//  [Mock file]: __mocks__/useDataApi.js
let data = {
    firstName: '',
    lastName: '',
    sendEmail: jest.fn()
}

export const setMockData = (newData) => {
    data = { ...newData, ...data }
}

export default jest.fn().mockImplementation(() => data)
```

```javascript
// [Jest spec file]: useDataApi.spec.js
import useDataApi, { setMockData } from '../../shared/hooks/useDataApi'

// mocking a hook that has a manual mock
jest.mock('../../shared/hooks/useDataApi')

describe('ComponentName)', () => {
    let mockApiData

    beforeEach(() => {
        mockApiData = {
            sendEmail: jest.fn(),
            firstName: 'Bob',
            lastName: 'Smith'
        }
        
        setMockData(mockApiData)
    })

    it('should send an email', () => {
        const email = 'bob.smith@jest.com'

        sut.props().onSubmit(email)

        expect(mockApiData.sendEmail).toHaveBeenCalledWith(email)
    })
})
```

#### Can also use 'spyOn'
```javascript
import useDataApi from '../../../shared/hooks/useDataApi'

jest.mock('../../../shared/hooks/useDataApi')

describe('ComponentName)', () => {
    let mockApiData

    beforeEach(() => {
        mockApiData = {
            sendEmail: jest.fn(),
            firstName: 'Bob',
            lastName: 'Smith'
        }
        
        just.spyOn(useDataApi, 'default').mockImplementation(() => mockApiData)
    })

    it('should send an email', () => {
        const email = 'bob.smith@jest.com'

        sut.props().onSubmit(email)

        expect(mockApiData.sendEmail).toHaveBeenCalledWith(email)
    })
```

#### 'toHaveBeenCalled___' function invocation
Use 'toHaveBeenCalled()' to test if the function was called without arguments or with redundant arguments.
'toHaveBeenCalledWith()' should be used for cases with arguments. It shouldn't be called without arguments.
'toHaveBeenCalledTimes()' can be used to check the number of times a function was called

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

    it('should invoke emailFunc()', () => {
        testFunction(correctArg)

        expect(emailFunc).toHaveBeenCalled()
    })

    it('should show console errors if testFunction was invoked with a wrong argument', () => {
        testFunction(wrongArg)

        expect(spyConsole).toHaveBeenCalledWith('Error: message')
    })
})

```

#### Use 'jest.resetAllMocks()' and 'jest.clearAllMocks()' in 'afterEach()' block
```javascript
describe('ComponentName)', () => {
    let spy

    beforeEach(() => {
        spy = jest.spyOn(console, 'error')
    })

    afterEach(() => {
        jest.clearAllMocks()
    })
})
```
