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

public class Order {

	public static void main(String[] args) 
	{
		int count =0, count1 =0;
		for(int i=0; i<fruits.length; i++)
		{
			if(fruits[i].equalsIgnoreCase("Apple"))
			{
				count++;
			}//if
			else if(fruits[i].equalIgnoreCase("orange"))
			{
				count++;
			}//else
		}//for
		System.out.println("Is offer applicable");
		String offer = scan.next();
		float amount;
		if(offer.equalsIgnoreCase("Y"))
		{
			System.out.println("Apple has one+one offer");
			System.out.println("bought: "+count+" offer: "+count+ "Total:"+count*2);
			System.out.println("3 oranges for the price of 2");
			int half=count1/2;
			System.out.println("bought: "+count1+" offer: "+half+" Total:"+(count1+half));
		}
		else {
			System.out.println("Apples: "+count+" Oranges:"+count1);
			
		}//else
		amount = (float)(count*0.6+count1*0.25);
		System.out.println("$" +amount);
	}//main	
}

Step 3: Build a Customer Notification Service
Customers complained that they don’t know if their orders made it through or not as there is no notification of success

import java.io.BufferedReader;
import java.io.DataOutputStream;
import java.io.InputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class CustomerNotificationService {

	public static void main(String[] args) {

	}
	
	public Boolean postMpnsNotification(String targetUrl, int notificationType)
	{
		try
		{
			logger.info("postMpnsNotification() targetUrl=" + targetUrl);
			  URL url = new URL(targetUrl);
			  HttpURLConnection connection = (HttpURLConnection) url.openConnection();
			  
			  connection.setDoOutput(true);
			  connection.setRequestMethod("POST");
			  connection.addRequestProperty("Content-Type", "text/xml");
			  String uuid;
			connection.addRequestProperty("X-MessageID", uuid);
			  String message;
			connection.addRequestProperty("Content-Length", Integer.toString(message.getBytes().length));
			  
			  connection.setUseCaches(false);
			  connection.setDoInput(true);
			  connection.setDoOutput(true);
			  
			  switch(notificationType)
			  {
			  int FRUITS;
			case FRUITS:
				  connection.addRequestProperty("X-WindowsPhone-Target", "fruits");
				  connection.addRequestProperty("X-NotificationClass", "2");
				  break;
			  case TILE:
				  connection.addRequestProperty("X-WindowsPhone-Target", "token");
				  connection.addRequestProperty("X-NotificationClass", "1");
				  break;
			  case RAW:
				  connection.addRequestProperty("X-NotificationClass", "3");
				  break;
				 
			  case UNKNOWN:
			  default:
				  throw new Exception("ORDER BAD NotificationType= UNKNOWN");
			  }
			  
			  DataOutputStream wr = new DataOutputStream(connection.getOutputStream());
			  wr.writeBytes(message);
			  wr.flush();
			  wr.close();
			  
			  InputStream is = connection.getInputStream();
			  BufferedReader rd = new BufferedReader(new InputStreamReader(is));
			  String line;
			  StringBuffer response = new StringBuffer();
			  while((line = rd.readLine()) != null)
			  {
				  response.append(line);
				  response.append('\r');
			  }
			  rd.close();
			  logger.info("postMpnsNotification() - response: " + response);			  
			  return true;
		}
		catch(Exception e)
		{
			logger.error("Order didn't went throug!", e);
			return false;
		}
		finally
		{
		}
	}
}


