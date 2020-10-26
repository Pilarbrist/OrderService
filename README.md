# OrderService

1.	Step 1: Build an Orders Service 
Build a service that’s able to receive simple orders of shopping goods from the command line.

package com.Express.Tests;
import java.util.Scanner;

public class OrdersService {

	public static void main(String[] args) 	
	{
	Scanner scanS = new Scanner(System.in);
	System.out.println("Enter input apple and orange using separated");
	String inputFruit = scanS.nextLine();
	String[] split = inputFruit.split(",");
	float sum = 0;
	for(int i = 0; i<split.length; i++)
	{
		if(split[i].equalsIgnoreCase("Apple"))
		{
			sum =(float)(sum+60);
		}
		else 
			if(split[i].equalsIgnoreCase("Orange")) 
			
				sum =(float)(sum+25);					
	}//for
	System.out.println("$" +sum);
	scanS.close();
	}
}


"Customer Notification Service"

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
			  int TOAST;
			case TOAST:
				  connection.addRequestProperty("X-WindowsPhone-Target", "toast");
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


