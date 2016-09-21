# appointment
import java.text.DecimalFormat;

public class Appointment
{
  //Initialize variables
  String name;
  String day, month, year;
  DecimalFormat timeFmt = new DecimalFormat("##.00");
  double time;
  boolean isItAM;
  
  //Constructor
  public Appointment()
  {
    name = "Default";
    day = "01";
    month = "01";
    year = "2014";
    time = 12.00;
    isItAM = true; 
  }
  
  //Constructor with parameters
  public Appointment(String nme, String dy, String mnth, String yr, double tme, boolean aMisIt)
  {
    this.name = nme;
    this.day = dy;
    this.month = mnth;
    this.year = yr;
    this.time = tme;
    this.isItAM = aMisIt;
  }
  
  //Retrieves name
  public String getName()
  {
    return this.name;
  }
  
  //Retrieves day
  public String getDayString()
  {
    return this.day;
  }
  
  //Retrieves month
  public String getMonth()
  {
    return this.month;
  }
  
  //Returns month as a name, not number
  public String getMonthString()
  {
    if (month.equals("01"))
      return ("January");
    if (month.equals("02"))
      return ("Feburary");
    if (month.equals("03"))
      return ("March");
    if (month.equals("04"))
      return ("April");
    if (month.equals("05"))
      return ("May");
    if (month.equals("06"))
      return ("June");
    if (month.equals("07"))
      return ("July");
    if (month.equals("08"))
      return ("August");
    if (month.equals("09"))
      return ("September");
    if (month.equals("10"))
      return ("October");
    if (month.equals("11"))
      return ("November");
    if (month.equals("12"))
      return ("December");
    else
      return "";
  }
  
  //Retrieves year
  public String getYearString()
  {
    return this.year;
  }
  
  //Retrieves time
  public double getTime()
  {
    return this.time;
  }
  
  //Retrieves AM or PM
  public boolean getAM()
  {
    return this.isItAM;
  }
  
  //Return AM or PM
  public String findAmPm()
  {
    if (this.isItAM)
      return "AM";
    else
      return "PM";
  }
  
  //print method for user input
  public void printAppt()
  {
    System.out.println("Your Appointment:\nName: " + name + "\nDate: " + this.getMonthString() + " " + this.getDayString() +
                       ", " + this.getYearString() + "\nTime: " + timeFmt.format(time) + " " + this.findAmPm());
  }
  

  //Appontment with parameter of type Appointment
  public Appointment duplicateAppt(Appointment appt)
  {
    Appointment newAppt = new Appointment(appt.getName(), appt.getDayString(), 
                                          appt.getMonth(), appt.getYearString(), appt.getTime(), appt.getAM());
    return newAppt;
  }
}


