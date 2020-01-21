# URLSessionPOSTandGET

# Post API Call and Parsing Using Encoder and Decoder

    func makePostCall() {
      
        let auth = "SDEybGpRS01vNUxoNXJzYkFoTnlqRkpObk9MekRTUzc5V0xObnhzZ1paNTRCVTB3SUtqd2JabTByVm9E5e26a5d45299a"
        
        let newTodo: [String : String] = ["email":emailTextField.text ?? "", "password":passwordTextField.text ?? "", "device_type": "1", "device_token":"1234567890"]
        
        
        let config = URLSessionConfiguration.default

        let session = URLSession(configuration: config)

        let url = URL(string: "http://php.sample.tk/staging/name_stag/api/login")!
        var urlRequest = URLRequest(url: url)
        urlRequest.httpMethod = "POST"
        //urlRequest.setValue(auth, forHTTPHeaderField: "Authorization")
        urlRequest.addValue("application/json", forHTTPHeaderField: "Content-Type")
        
        print(newTodo)

        guard let postData = try? JSONSerialization.data(withJSONObject: newTodo, options: []) else {
            return
        }

        urlRequest.httpBody = postData

        let task = session.dataTask(with: urlRequest) { data, response, error in
            
            // ensure there is no error for this HTTP response
            guard error == nil else {
                print ("error: \(error!)")
                return
            }
            
            // ensure there is data returned from this HTTP response
            guard let content = data else {
                print("No data")
                return
            }
            print(content)
            
//            // serialise the data / NSData object into Dictionary [String : Any]
//            guard let json = (try? JSONSerialization.jsonObject(with: content, options: JSONSerialization.ReadingOptions.mutableContainers)) as? [String: Any] else {
//                print("Not containing JSON")
//                return
//            }
//            print(json)
     
            // update UI using the response here
            let user = try! JSONDecoder().decode(Welcome.self, from: data ?? Data())
            print(user.userData?.country?.name ?? "")
            
          
            
            
        }

        // execute the HTTP request
        task.resume()
    }
    
    
    
    #GET API CALL USING URL SESSION
    
            func makePostCall() {
          
            let auth = "RzR2dnBQVFJkODJ2RjZKRzFDTkl1UUg2T243RE1BVjNPaXBIVDliTVZIbmd4ZmF2cVpzOHF4eDllN1pL5e26c7afd448a"
          
            let config = URLSessionConfiguration.default

            let session = URLSession(configuration: config)

            let url = URL(string: "http://php.sample.tk/staging/name_stag/api/getDashboardData")!
            var urlRequest = URLRequest(url: url)
            urlRequest.httpMethod = "GET"
            urlRequest.setValue(auth, forHTTPHeaderField: "Authorization")
            urlRequest.addValue("application/json", forHTTPHeaderField: "Content-Type")
         

            let task = session.dataTask(with: urlRequest) { data, response, error in
                
                // ensure there is no error for this HTTP response
                guard error == nil else {
                    print ("error: \(error!)")
                    return
                }
                
                // ensure there is data returned from this HTTP response
                guard let content = data else {
                    print("No data")
                    return
                }
                print(content)
                
                // serialise the data / NSData object into Dictionary [String : Any]
//                guard let json = (try? JSONSerialization.jsonObject(with: content, options: JSONSerialization.ReadingOptions.mutableContainers)) as? [String: Any] else {
//                    print("Not containing JSON")
//                    return
//                }
//                print(json)
         
                // update UI using the response here
                let user = try! JSONDecoder().decode(Welcome.self, from: data ?? Data())
                print(user.dashboardData.reamingInGl)
              
            }

            // execute the HTTP request
            task.resume()
        }
    
    
    
