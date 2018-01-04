# OO-Ruby-Evening-notes
```
# classes are like factories that they create invidual objects or instances of the class
# for example a Dog class would create an individual dog who might have a name, age, and a breed

# the initialize method is called whenever we create a new instance of a class. It's basically like what kind of details do we want to give this instance right out of the box? Do we want this dog to have a name, an age, and a breed right at the time this dog is born?

# Argument values get sent to the initialize method when .new is called, so for example if we had def initialize(name, age, breed), we would instantiate the dog with Dog.new('fido', 1, 'mutt')

# When assigning values like name / age / breed and for our entire instance to know about we use @instance variables. Instance variables are like any other variable where it stores values, however it's more on a global scope of your instance you've created. Meaning all the instance methods you've created inside your class will know about the instance variables without having to pass them in as arguments.

# we use writer / setter methods in order to change instance variables. Which helps when we aren't coding inside our class but using our instance elsewhere.

# we use reader / getter methods in order to use the values of the instance variables outside of the class scope.

# You can however use both of these methods (writer / reader) also in your class.

# self is a way to describe what is calling the method. If it's an instance method, then self will refer to the instance that is calling the method. If it's a class method then self will refer to the class that is calling it.

# class methods are methods that would not be used by an instance or pertains to an instance. You can do things like keep track of all your instances, keep a count of all your instance, etc...

# class methods are defined with self.method_name as the method name.

# class @@variables are set once ruby reads the class for the first time. So before any instance is created it will have those variables created. For instance if you created a class variable to store your objects you might have @@all = [] defined in your class. Then you could make a class method like def self.all that just returns @@all. To call this method if it was defined in a Dog class, you would call it like Dog.all to get that array.

class Pet
  # gives both reader / writer methods
  @@all = []
  attr_accessor :name, :age, :breed, :owner
  # attr_writer :name
  # attr_reader :name
  
  def initialize(name, age, breed)
    @name_of_user = name
    @age = age
    @breed = breed
  end
  
  def save
    self.class.all.push(self)
  end
  
  def self.create(name, age, breed)
    pet = self.new(name, age , breed)
    pet.save
    pet
  end
  
  def self.all
    @@all
  end
  
  # def name=(name)
  #   @name_of_user = name
  # end
  
  # def name
  #   @name_of_user
  # end
end

class Owner
  attr_accessor :name, :pets
  @@all = []
  
  
  def initialize(name)
    # instance method
    # self refers to the instance
    self.name = name
    self.pets = []
  end
  
  def add_pet(pet)
    self.pets.push(pet)
  end
  
  def save
    self.class.all.push(self)
  end
  
  def self.create(name)
    owner = self.new(name)
    owner.save
    owner
  end
  
  def self.all
    # self in a class method refers to the class, example Owner
    # self being part of the method name creates it as a class method
    @@all
  end
end

fido = Pet.create('Fido', 1, 'Mutt')
fido.name = 'Dover'
fido.name # return 'Dover'
bob = Owner.create('Bob')
fido.owner = bob
bob.add_pet(fido)
bob.pets.each do |pet|
  puts "pet name: #{pet.name}"
  puts "pet age: #{pet.age}"
  puts "pet breed: #{pet.breed}"
end
puts fido.owner.name
```
