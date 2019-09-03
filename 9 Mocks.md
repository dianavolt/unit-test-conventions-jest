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
