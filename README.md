# SwiftExamples
> I this repository I try to note Swift code control of follows with Example

1.  swift array and set of types conversion to each another
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
2. Create a file into document directory of user domain mask (user folder)

```swift
let file = "file.txt" //this is the file. we will write to and read from it
        let text = "some text" //just a text
        if let dir = FileManager.default.urls(for: .documentDirectory, in: .userDomainMask).first {
            print(dir)
            let fileURL = dir.appendingPathComponent(file)

            //writing
            do {
                 try text.write(to: fileURL, atomically: false, encoding: .utf8)
            }
            catch {print(error)}

            //reading
            do {
                let text2 = try String(contentsOf: fileURL, encoding: .utf8)
            }
             catch {print(error)}
        }
```

3. Create Property List on user domain mask
```swift
let data : [String: String] = [
                       "Company": "My Company",
                       "FullName": "My Full Name",
                       "FirstName": "My First Name",
                       "LastName": "My Last Name",
                   ]
        let someData = NSDictionary(dictionary: data)


       /* Crate plist at document directory at user domain mask */
        let fileManager = FileManager.default

        let documentLocation = NSSearchPathForDirectoriesInDomains(.documentDirectory, .userDomainMask, true)[0] as String
        let path = documentLocation.appending("profile.plist")
        if(!fileManager.fileExists(atPath: path)){
            print(path)

            let isWritten = someData.write(toFile: path, atomically: true)
            print("is the file created: \(isWritten)")
        }else{
            print("file exists")
        }
        /* Fetch property list */
        if let profile = NSDictionary(contentsOfFile: path) as? [String: String] {
              print("profile = \(profile)")
        }
        
        // Using URL
         let fileManager = FileManager.default
        // Create file at document directory of user mask
        let documentLocation = fileManager.urls(for: .documentDirectory, in: .userDomainMask)[0] as URL
        let target = URL(fileURLWithPath: "profile.plist", relativeTo: documentLocation)
        let isWritten = someData.write(to: target, atomically: true)
         print("is the file created: \(isWritten)")
        
        /* Fetch plist with serialized data*/
        let directory = FileManager.default.urls(for: .documentDirectory, in: .userDomainMask)[0]
        let fileURL = URL(fileURLWithPath: "profile.plist", relativeTo: directory)
            do{
                 let data = try Data(contentsOf: fileURL)
                 let fetchData = try PropertyListSerialization.propertyList(from: data,  format: nil) as? [String: String]
                print(fetchData ?? "Not found")
            }catch{ print(error) }
```
4, Access file(Property List) from Main bundle
```swift
      let bundleDirectory = Bundle.main.path(forResource: "Documentsprofile", ofType: "plist")
        if let profile = NSDictionary(contentsOfFile: bundleDirectory!) as? [String: String] {
                      print("profile = \(profile)")
         }
        
        // Fetch config plist form main apps bundle
        if let url = Bundle.main.url(forResource:"Documentsprofile", withExtension: "plist") {
           do {
             let data = try Data(contentsOf:url)
             let swiftDictionary = try PropertyListSerialization.propertyList(from: data, format: nil) as! [String:Any]
              print(swiftDictionary)
           } catch {
              print(error)
           }
        }
        ```
