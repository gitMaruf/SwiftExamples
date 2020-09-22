# SwiftExamples
I this repository I try to note Swift code control of follows with Example

swift array and set of types conversion to each another
```swift
import UIKit

struct Employee: Hashable{
    let name: String
    let id: UUID
    let age: Int
}
class ViewController: UIViewController {
    
    var employeeSet: Set<Employee> = []
    var employeeArray: [Employee] = []
    override func viewDidLoad(){
        super.viewDidLoad()
        
       employeeArray.append(Employee(name: "O Brain", id: UUID(), age: 1))
       employeeArray.append(Employee(name: "Joe Smith", id: UUID(), age: 2))
       employeeSet.insert(Employee(name: "Ken", id: UUID(), age: 3))
       employeeSet.insert(Employee(name: "Martin", id: UUID(), age: 4))
      
     // comvert employee set to array
//        employeeSet.forEach({ perEmployee in
//            employeeArray.append(perEmployee)
//        })
//          print("Employee array is \(employeeArray)")
        
    // convert employee set to employee array
        employeeArray.forEach({perEmployee in
            employeeSet.insert(perEmployee)
        })
        
        print("Employee set is \(employeeSet)")
    }
}

```
