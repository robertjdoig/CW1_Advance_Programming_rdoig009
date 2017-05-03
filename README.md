# CW1_Advance_Programming_rdoig009

# Hacker Rank Overview 

I chose to completely some of the C++ HackerRank challenges. I started by working my way through from the start. I have chosen four examples of the challenges that I have completed with an explanation of what I learnt from completely the challenge. My score at the time of writing this report is 452.5 points. Please see the image below for the proof of this score.

## 1. Virtual Functions 

This challenge was based on virtual functions are used within inherited classes. This was in the form of a Person, Professor and Student class. The Person class was the base class which stores the data of the members name and age. The Professor and Student inherit from the Person class, which use the stored data and the additional marks or current ID within the virtual functions.  

This challenge was relatively simple to solve. The base class just initializes the virtual class and the inherited class define what the function should do. 

    class Person{
      protected:
      string name;
      int age;

      public:
      virtual void getdata(){}
      virtual void putdata(){}
    };  

    class Professor : public Person{
      int publications;
      int cur_id = 1;
    
      void getdata(){
         cin >> name >> age >> publications;
        
         static int professor_count; 
         professor_count++; 
         cur_id = professor_count;
      }
    
      void putdata(){
         cout << name << " " << age << " " << publications << " " << cur_id << endl; 
      }
    };
    
    class Student : public Person{
      int marks[6];
      int cur_id;
    
      void getdata(){
        
         cin >> name >> age;
        for(int i; i < 6; i++){
           cin >> marks[i];
        }
       
       static int student_count;
       student_count++;
        
       cur_id = student_count;
    }
    
    void putdata(){
        int sum = 0;
        for(int i = 0; i < 6; i++){
          sum += marks[i];
        }
        cout << name << " " << age << " " << sum << " " << cur_id << endl; 
    }
    
    };
    
    
## 2. Inherited Code

In this problem the inherited code has an invalid username validation function. It throws an exception which is not handled. This causes the program to exit without any message. The code that is inherited is locked and can not be edited so an exception extension is needed. 

The class reads in the exception which is passed into to the BadLengthException constructor. After the exception is constructed then the function 'What' is called. 'What' takes the exception and concatenates the exception into a std::string. This is then returned so the exception can be printed successfully.     
    
    class BadLengthException : public exception{

    private:
      int n;
    
    public:
      BadLengthException(int N){ n = N; }
    
      virtual const char * what(){
          return std::to_string(n).c_str();
      }
    };
    
## 3. Exceptional Server

The problem in exceptional servers is that the server is throwing an exception which has not been handled yet. This could be of three different types, not enough memory, an exception message and any non standard cases. This solution simply tries the computation of A and B with printing out the answer. Since it is wrapped with  the try statement when it fails it falls through to the catch statements underneath. Each of these statement handle the different types of exceptional that have been thrown. 

        try
        {
            Server s;
            long long R = s.compute(A,B);
            cout << R << endl;
        }

        catch(bad_alloc&){ cout << "Not enough memory" << endl; }
        catch(exception &e){ cout << "Exception: " << e.what() << endl; }
        catch(...){ cout << "Other Exception" << endl; }


## 4. Accessing Inherited functions

With this problem you have to implement a function which updates the value using either A, B or C classes implementation of this function. If the number is divisible by 2, 3, 5 then use A, B or C respectively. This was simply solved by checking the incoming numbers, if the number was divisible using the modulus to check if it was divided into perfectly. Afterwards the function from each class is called. 

    class D : public A, public B, public C
    {
    	int val;
    	public:
    	//Initially val is 1
    	D()
    	{
    		val=1;
    	}
    	//Implement this function
    	void update_val(int new_val)
    	{
    		while((new_val / val) % 2 == 0){ 
                    		A::func(val); 
                		}
                		while((new_val / val) % 3 == 0){ 
                 	 	B::func(val); 
                		}
                		while((new_val / val) % 5 == 0){ 
                    		C::func(val); 
                		}    	
    	}
                //For Checking Purpose
                void check(int); //Do not delete this line.
    };
   
   
   
   
## Global Games Jams 2017

Video Link: https://www.youtube.com/watch?v=Nblo7VLYo1U

The key word for this games jam was waves. It was a very nice topic as there are multiple different meanings and assets which can be classified as a wave form.  

In the initial brainstorm, I had thought of having an environment which pulsed and was effected by waves. This would be changed by the users bouncing or jumping on this environment which would send shock waves thought to the other person. On further refinement of the idea we settled on ocean waves which would effect the player's boats which would make it harder for them to collect the coins that would spawn around the map. We wanted this game to be a simple couch game where two or more players could pick up a controller and battle against each other to collect as many coins as possible. 

When talking about how to implement this game we landed on three main problem areas. Wave simulation, player movement and boat physics. We separated the initial problems between each of us. I was doing the environment which changes with the waves that we apply to it. With Witek and Nikita starting on the boats movement and physics. 

I started with a cube grid which was effected with a basic sine wave. When the design team had settled on water as the landscape we changed it to a plane mesh. This also solved some problems with performs as 10x10 grid was 100 cubes. This grew too fast for a decently sized map. Once changed over it worked up to a 50 x 50 without any problems. This only started to become a problem when the weather effects were adding up. 

After the initial build and testing off the game, three more tasks were found. Weather system, player movement to work with a controller and a better boat buoyancy. On this sprint I was focusing on the players movement with a controller. We wanted it to be only the joystick so it was the simplest controls we could think of. However combining this with forces was tricky as we needed to rotate the ship to the same position as the analog stick. This was done by calculating how much torque was needed to change from its current position to the new one. On top of this we had to move the ship forwards. This we had to add an offset as otherwise the ship would nose dive or spin around and over. 

There was also some problems with the xbox controllers when disconnecting and reconnecting the controllers. Unity changes which port that the controller is connected to. This meant that the controller could be seen as 1, 2, 3 or 4 from within unity. This became a big problem that we did not have enough time to fix within the games jam. 
    
