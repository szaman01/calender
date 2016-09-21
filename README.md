# ScheduleMaster
//ScheduleMaster.java                Author: Shafin Zaman

import java.util.*;
import java.text.DecimalFormat;
import java.io.*;

public class ScheduleMaster
{
  public static void main (String [] args) throws IOException
  {    
    Scanner scan = new Scanner(System.in);
    DecimalFormat timeFmt = new DecimalFormat("##.00");
    
    //Welcome Banner
    System.out.println(" ___________________________________________________________________________");
    System.out.println("|                                                                           |");
    System.out.println("|                        WELCOME TO SCHEDULE MASTER                         |");
    System.out.println("|                                                                           |");
    System.out.println("|___________________________________________________________________________|");
    
    System.out.println(" ____________________________________________________________________________");
    System.out.println("|          |          |          |          |          |          |          |");                                                          
    System.out.println("|     1    |     2    |     3    |     4    |     5    |     6    |     7    |");
    System.out.println(" ____________________________________________________________________________");
    System.out.println("|          |          |          |          |          |          |          |");                                                               
    System.out.println("|     8    |     9    |    10    |    11    |    12    |    13    |    14    |");
    System.out.println(" ____________________________________________________________________________");
    System.out.println("|          |          |          |          |          |          |          |");                                                               
    System.out.println("|    15    |    16    |    17    |    18    |    19    |    20    |   21     |");
    System.out.println(" ____________________________________________________________________________");
    System.out.println("|          |          |          |          |          |          |          |");                                                               
    System.out.println("|    22    |    23    |    24    |    25    |    26    |    27    |   28     |");
    System.out.println(" ____________________________________________________________________________");
    System.out.println("|          |          |          |          |          |          |          |");                                                               
    System.out.println("|    29    |    30    |    31    |          |          |          |          |");
    System.out.println(" ____________________________________________________________________________");
    
    //Inputfile
    Scanner inputScan = new Scanner (new File("Intro.txt"));
    while (inputScan.hasNext())
    {
      System.out.println(inputScan.nextLine());
    }
    System.out.println("");
    
    //Prompt user to make an appointment
    System.out.println("How many appointments would you like to make?");
    int count = scan.nextInt();
    scan.nextLine();
    
    //Declare Array
    Appointment[] apptArry = new Appointment [count];
    
    for (int i = 0; i<count; i++)
    {
      
      //Prompt user to enter name, date, time and whether or no it is in the AM or PM
      System.out.println("Please enter the name of the appointment");
      String name = scan.nextLine();
      
      System.out.println("Please enter the date of the appointment in dd/mm/yyyy format");
      String date = scan.nextLine();
      String day = date.substring(0,2);
      String month = date.substring(3,5);
      String year = date.substring(6);
      
      System.out.println("Please enter the time of the appointment");
      System.out.println("Please write it as a decimal. Example: 12.30");
      double time = scan.nextDouble();
      scan.nextLine();
      System.out.println("Is the appointment in the AM or PM?");
      System.out.println("Enter AM or PM");
      boolean isItAM;
      if (scan.nextLine().equalsIgnoreCase("AM"))
        isItAM = true;
      else 
        isItAM = false;
      
      //Object of class Appointment
      Appointment appt = new Appointment(name, day, month, year, time, isItAM);
      apptArry[i] = appt;
      appt.printAppt();
    }
    
    //Sort Array
    Appointment[] arr = new Appointment[count];
    arr = sortIt(apptArry); 
    
   //Print out sorted array
    for (int p = 0; p < arr.length; p++)
    {
      arr[p].printAppt();
    }
    
    int monthRan = (int) ((Math.random()*12) + 1); 
    
    String monthString = monthRan + "";
    
    System.out.println("The random month generated was " + convertMonth(monthRan));
    
    //searchArrayForThisMonth
    boolean targetFound = false;    
    targetFound = searchForMonth(arr, monthString);
    
    if (targetFound)
    {
      System.out.println("This month is in the array.");
    }
    else
    {
      System.out.println("This month is not in the array.");
    }
    
    //Outputfile
    PrintWriter writer = new PrintWriter("AppointmentList.txt");
    writer.println("Appointment List");
    for (int j = 0; j < arr.length; j++)
    {
      writer.println("Your Appointment:");
      writer.println("Name: " + arr[j].getName());
      writer.println("Date: " + arr[j].getMonthString() + " " + arr[j].getDayString() +
                       ", " + arr[j].getYearString());
      writer.println("Time: " + timeFmt.format(arr[j].getTime())+ " " + arr[j].findAmPm());
      writer.println("");
    }
    writer.close();
  }
  
  // Search method
  public static boolean searchForMonth(Appointment[] array, String month)
  {
    if (month.length() == 1)
    {
      month = "0" + month;
    }
    
    for (int r = 0; r < array.length; r++)
    {
      
      if (array[r].getMonth().equals(month))
      {
        return true;
      }
      
    }
    return false;
  } 
  
  //sorting method by year
  public static Appointment[] sortIt(Appointment[] apptArry)
  {
    //sort by year
    int k;
    int tempOne, tempTwo;
    for (int m = apptArry.length; m >= 0; m--) {
      for (int i = 0; i < apptArry.length - 1; i++) {
        k = i + 1;
        tempOne = Integer.parseInt(apptArry[i].getYearString());
        tempTwo = Integer.parseInt(apptArry[k].getYearString());
        if (tempOne > tempTwo) 
        {
          swapNumbers(i, k, apptArry);
        }
      }
    }
    
    return apptArry;
  }
  
  //Swap method
  public static void swapNumbers(int i, int j, Appointment[] array) {
    
    Appointment temp;
    temp = array[i];
    array[i] = array[j];
    array[j] = temp;
  }
  
  
  
  public static String convertMonth(int month)
  {
    switch (month)
    {
      case 1:
      {
        return "January";
      }
      case 2:
      {
        return "February";
      }
      case 3:
      {
        return "March";
      }
      case 4:
      {
        return "April";
      }
      case 5:
      {
        return "May";
      }
      case 6:
      {
        return "June";
      }
      case 7:
      {
        return "July";
      }
      case 8:
      {
        return "August";
        
      }
      case 9:
      {
        return "September";
      }
      case 10:
      {
        return "October";
      }
      case 11:
      {
        return "November";
      }
      case 12:
      {
        return "December";
      }
      default:
      {
        return "";
      }
      
    }
  }
}













