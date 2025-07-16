# Vending-Machine-Controller

- In this project, I have designed and implemented Vending Machine Controller using VHDL using Quartus Prime and Modelsim software.

### 1. INTRODUCTION  
***

Vending Machine is an electronic machine used to dispense a product to a consumer after a prescribed amount of money has been put into the machine. Considering the current situation, the three most important things we need when we are outside are sanitizer, tissue paper, and paper soap for cleanliness and sanity purposes. So, we are designing a Vending Machine Controller using VHDL for sanitizer, tissue paper, and paper soap. This machine can be used at various places like railway station, food stalls, etc.  

The FPGA based Vending machines are reprogrammable, flexible, and more advantageous in terms of speed, response and power consumption. FPGA based machine can be reprogrammed without the need to change the whole architecture when enhancing the model of machine. Microcontroller executes all operations in a sequential fashion whereas an FPGA is a field programmable gate array which will execute all your operations in parallel fashion. 

### 1.1 FSM (Finite State Machine) [2] [3] 
***
In a Finite State Machine, the circuit’s output is defined in a different set of states i.e. each output is a state. A State Register to hold the state of the machine and a next state logic to decode the next state. An output register defines the output of the machine. In FSM based machines the hardware gets reduced as in this the whole algorithm can be explained in one process.   


### 3. IMPLEMENTATION OF VENDING MACHINE  
***
![image](https://user-images.githubusercontent.com/70748543/152948761-ef846dd2-e0aa-4e93-8c45-e13c0790c43f.png)
                                                  
Figure 3: Block Diagram  

Vending machine for Sanitizer, tissue paper, and paper soap is designed using Quartus Prime Software. It can be deployed in the form of VHDL code, RTL view, and output waveform. The system will accept 3 inputs sanitizer, tissue paper, and paper soap, and will give the total cost. The complete cycle will run around 6 states idle, select item, review, payment status, refund, and delivered. If the amount is more than cost price change is returned and if the amount is less than the cost price complete amount is returned with no delivery. 


### 4. DESIGN METHODOLOGY  
***
![image](https://user-images.githubusercontent.com/70748543/152948919-adfb72c2-ad4c-413d-b6d3-9fe6872491af.png)

The code will accept three inputs and system will run around 5 states idle, select\_item, review, payment\_status, and refund. Initially it will be at idle state and after each clock cycle it will change its state. Next state will be select\_item state where you can individually select from the given inputs and then it will go to review state where it will give you the total amount so you can check whether it is correct or not. If the total amount is correct it will go to payment\_status state where you can enter the amount and it will then go in the refund based on comparing it with the total amount. If the cost entered is less than the total cost then it will refund the complete entered amount and will give no delivery similarly if the cost entered is more than than total cost it will refund the change and give the delivery.    

**Description of states**  
The selection of products and all the states is shown below: 

when idle =>  p_s  <= select_item ; 

when select_item => 

temp  := (10 *sanitizer + 5  *tissue_paper + 1 *paper_soap ); 

total <= temp ;

p_s <= review ; 

when review  => 

if (proceed ='1')  then 

p_s <=  payment_status; 

elsif(proceed = '0' )  then 

p_s <= select_item ; end if ;  

when payment_status => 

if (temp <= coin_in) then 

delivered <= '1' ; 

p_s  <= refund ;

elsif(temp > coin_in ) then

delivered <= '0' ; 

coin_out <= coin_in ; 

p_s <= payment_status;

end if ; 

when refund => coin_out <= coin_in-temp; 

Similarly, we can add other products also. 

### 5. SIMULATION RESULTS
***
The Simulation is done using Modelsim software. Initially the reset is set to 0 and clock signal is given and then the state changes from idle to select\_item state where I have selected 5 sanitizer, 5 tissue paper and 5 paper soap. According to the pre-defined formla the total amount must be 80 and we have received the same in the review state then we set proceed to 1 and state changes to payment state where I have considered three different cases. 

1. In the first case I have set the coin in to 70 which is less than the total amount so according to the code it must redurn the whole amount i.e. 70 in the refund section and delivered signal must be 0 and we have successfully got the same results. 
1. In the second state the coin in input is set to 100 which is more than the total amount hace it must return 20 in the refund section and the delivered signal must become 1 and we have successfully got the results of the 2nd case correctly 
1. Now, in the third state I have considered an idle state where we have entered the correct coin in amount which is 80 and hence it should return 0 in the refund section and delivered signal must be 1 and here also we have successfully got the correct results. 

![image](https://user-images.githubusercontent.com/70748543/152949593-7f31aeb5-73eb-4511-9d85-0e55be1993da.png)

The below figure shows the complete RTL view: 

![image](https://user-images.githubusercontent.com/70748543/152949733-5dbdaeac-17f9-4ac1-927e-e3ca5745e852.png)

Figure 4: RTL View 

I have divided the RTL view in two sections in the below figure as input and output part of the RTL view. 

![alt-text-1](https://user-images.githubusercontent.com/70748543/152949809-6553386c-cee8-4144-a05f-e017840c09ab.png "Figure-5" )          

**Figure 5**: Input Section  

 ![alt-text-1](https://user-images.githubusercontent.com/70748543/152949878-20b69509-5fd9-4658-ba9b-e655b6bb5942.png "Figure-6")
