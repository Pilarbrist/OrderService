# OrderService

Step 1: Build an Orders Service 
•	Build a service that’s able to receive simple orders of shopping goods from the command line 
•	Apples cost 60 cents and oranges cost 25 cents 
•	The service should be able to calculate that: 
• [ Apple, Apple, Orange, Apple ] => $2.05 
•	Make reasonable assumptions about the inputs to your solution; for example, 
candidates may take a list of strings as input 
•	Add unit tests that validate your code 
Step 2: Simple offer 
•	The shop decides to introduce two new offers 
•	buy one get one free on Apples 
•	3 for the price of 2 on Oranges 
•	Update your functions & unit tests accordingly 


package com.Express.Tests;
import java.util.*;

public class Order 
{
	static int appleCount = 4;
	static int orangeCount = 550;
	
	public static void main(String[] args) 
	{
		Scanner scan = new Scanner(System.in);
		String input = scan.next();
		String fruits[] = input.split(",");
		int count =0, count1 =0;
		
		
		for(int i=0; i<fruits.length; i++)
		{
			if(fruits[i].equalsIgnoreCase("Apple"))
			{
				count++;
			}//if
			else if(fruits[i].equalsIgnoreCase("orange"))
			{
				count1++;
			}//else
		}//for
		if(count>appleCount || count1>orangeCount)
		{
		System.out.println("No stock !!! \nYour order failed");
		return;
		}
		System.out.println("Is offer applicable");
		String offer = scan.next();
		float amount;
		
		if(offer.equalsIgnoreCase("Y"))
		{
			int ctr = count * 2, half = count1 / 2;
			if(ctr > appleCount || (half+count1) > orangeCount)
			{
				System.out.println("No stock !!! \nYour order failed");
			}
			System.out.println("Apple has one+one offer");
			System.out.println("bought: "+count+" offer: "+count+ "Total:"+ctr);			
			System.out.println("3 oranges for the price of 2");
			System.out.println("bought: "+count1+" offer: "+half+" Total:"+(count1+half));
		}
		else 
		{
			System.out.println("Apples: "+count+" Oranges:"+count1);
			
		}//else
		amount = (float)(count*0.6+count1*0.25);
		System.out.println("$" +amount);
		System.out.println("Your order is completed!! will be delivered in 30 minutes.\nTankyou please visit again");
	}//main	
}
