# Json-data


import UIKit

class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        
        let url = URL(string: "http://gnb.dev.airtouchmedia.com/rates.json")
        let task  = URLSession.shared.dataTask(with: url!) { (data, response, error) in
        
        if error != nil
             {
            print("ERROR")
        }
        else {
            if let content  = data  {
                do {
                    
                    //Array
                    let myJson = try JSONSerialization.jsonObject(with:content, options: JSONSerialization.ReadingOptions.mutableContainers) as AnyObject
                    //print(myJson)
                    if let rate  = myJson["rate"] as? NSDictionary {
                     
                        if let currency = rate["USD"] {
                            print(currency)
                        }
                    }
             }
                catch {
                    
                }
            }
            }
        }
        task.resume()
    }

    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }


}


