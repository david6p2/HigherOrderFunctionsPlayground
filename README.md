##//Problems from http://www.weheartswift.com/higher-order-functions-map-filter-reduce-and-more/
###//1. Write a function that takes a function f and a float x and aplies f to x twice i.e. f(f(x))
    func applyTwice(f: ((Float) -> Float), x: Float) -> Float {
      return f(f(x))
    }

    func square(a:Float) -> Float {
      return a * a
    }

    applyTwice(f: square, x: 3)

###//2. Write a function that takes a function f and a float x and aplies f to x k times
#####//recursive version

    func applyKTimesRecursive(f:((Float) -> Float),x:Float,k:Int) -> Float {
      return k > 0 ? applyKTimes(f: f, x: f(x), k: k-1) : x
    }

Non recursive

    func applyKTimes(f:((Float) -> Float),x:Float,k:Int) -> Float {
      var y : Float = x
      for _ in 0..<k {
        y = f(y)
      }
      return y
    }

###//3. Using applyKTimes write a function that raises x to the kth power

    func raisesX(_ x:Float, toTheKthPower k:Int) -> Float{
      return applyKTimesRecursive(f: {x * $0}, x: 1, k: k)
    }

    raisesX(2.0,toTheKthPower: 2)

###//4. Given an array of Users which have properties name:String and age:Int
###//write a map function that returns an array of strings consisting of the user’s names

    class User : NSObject {
      var name : String?
      var age : Int?
      
      init(name: String, age: Int) {
        self.name = name
        self.age = age
      }
      
      override var description: String{
        return "name: \(name!), age: \(age!)"
      }
    }

    var userDavid = User(name: "David", age: 32)
    var userClara = User(name: "Clara", age: 33)
    var userPepe = User(name: "Pepe", age: 24)
    var users = [userDavid, userClara, userPepe]
    let names = users.map({"\($0.name!)"})

    print(names)

###//5. Given an array of of dictionaries containing keys for “name” and “age”
###//write a map function that returns an array of users created from it

    var usersDicts = [["name":"David", "age":32], ["name":"Clara", "age":33], ["name":"Pepe", "age":24]]

    var arrayOfUsers = usersDicts.map({User(name:$0["name"] as! String, age:$0["age"] as! Int)})
    print(arrayOfUsers)

###//6. Given an array of numbers write a filter method that only selects odd integers

    var numbers = [0,1,2,3,4,5,6,7,8,9,10,11,12]

    var oddNumbers = numbers.filter({$0%2 != 0})

    print(oddNumbers)

###//7. Given an array of strings write a filter function that selects only strings that can be converted to Ints

    var strings = ["0","cat","2","dog","car","7"]

    var intNumbers = strings.filter({(Int($0) != nil)})

    print(intNumbers)

###//8. Given an array of UIViews write a filter function that selects only those views that are a subclass of UILabel

    var view1 = UIView()
    var view2 = UITextView()
    var view3 = UIImageView()
    var view4 = UILabel()
    var view5 = UIScrollView()

    var views = [view1,view2,view3,view4,view5]

    var subclassesOfUIlabelViews = views.filter({$0.isKind(of: UILabel.self)})

    print(subclassesOfUIlabelViews)

###//9. Write a reduce function that takes an array of strings 
###//and returns a single string consisting of the given strings separated by newlines

    var animals = ["cat","dog","car","bird"]

    var sentence = animals.reduce("",{"\($0)\($1)\n"})

    print(sentence)


###//10. Write a reduce function that finds the largest element in an array of Ints

    var moreInts = [0,1,20,3,4,5,6,7,80,9,89,11,12]

    var largestElement = moreInts.reduce(Int.min, {$0>$1 ? $0 : $1})

    print(largestElement)

###//11. You could implement a mean function using the reduce operation
###//{$0 + $1 / Float(array.count)}. Why is this a bad idea?
    var array = [1,2,3,4,6]
    var mean = array.reduce(0, {($0+Float($1))/Float(array.count)})

    print("This \(mean) is not the real mean because it is adding each pair and dividing it by the \narray.count and then the result is added to the next element in the array and divided by \narray.count an so on")
