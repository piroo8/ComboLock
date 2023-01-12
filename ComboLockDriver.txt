package ComboLockDriver;

import java.util.Scanner;

public class ComboLockDriverIshP 
{
  public static void main(String[] args) 
  {
    ComboLockIshP comboLock = new ComboLockIshP();
    
    printProgramDescription();
    simulateComboLockDriver(comboLock);
  }
  /**
   * Prints out program description to the user
   */
  public static void printProgramDescription()
  {
    //Prints Program Description
    System.out.println("Lock Simulator 3000\nHello! \nThis program will allow you to simulate opening a combination lock with either\nA randomly generated 3 number combination or with a Lock Combination you set.");
  }
  public static void simulateComboLockDriver(ComboLockIshP comboLock)
  {
    int[] combo = new int[3];
    int comboType,option;
    boolean isLockSimulationOver = true;
    
    do
    {
      comboType = selectTypeOfCombination();
      combo = setLock(comboLock,comboType);
      simulateUnlockAttempt(comboLock,combo);
      option = getOptionToRepeat();
      
      if (option == 2)
      {
        isLockSimulationOver = false;
      }
      
    }while(isLockSimulationOver);
  }
  public static int selectTypeOfCombination()
  {
    Scanner input = new Scanner(System.in);
    String numStr = "", errMsg;
    int num = 0;
    boolean notValidInput = true; 
    
    do
    {
      System.out.println("\nYou have 2 options for your 3 digit lock Combination (where each digit is between 1-3): \nYou can either\n[Pick Your Own Combination: 1]\n[Choose a randomly Generated Combination: 2]");
      System.out.println("\nPlease pick one of the above option for your lock.");
      numStr = input.nextLine();
      
      errMsg = "Sorry, \" " + numStr + " \" is not an integer between 1 to 2\n";
      
      try
      {
        num = Integer.parseInt(numStr); // Convert the number from a String to an double
        
        if (num < 1 || num > 2)
        {
          num = Integer.parseInt("Error");
        }
        
        notValidInput = false;
      }                              
      catch (NumberFormatException error)  
      {
        System.out.println(errMsg);
      }
      
    }while(notValidInput);  // As long as input is a negative, repeat
    
    return num;
  }
  public static int[] setLock(ComboLockIshP comboLock,int comboType)
  {
    int[] combo = new int[3];
    
    if (comboType == 2)
    {
      // define the range 
      int max = 3; 
      int min = 1; 
      int range = max - min; 
      
      // generate random numbers within 0 to max 
      for (int i = 0; i < combo.length; i++) 
      {
        combo[i] = (int)(Math.random() * range+1);
      }
    }
    else
    {
      for (int i = 0; i < combo.length; i++) 
      {
        combo[i] = getSingleDigit(i+1);
      }
    }
    
    comboLock.setLock(combo);
    
    return combo;
  }
  public static int getSingleDigit(int i)
  {
    Scanner input = new Scanner(System.in);
    String numStr = "", errMsg;
    int num = 0;
    boolean notValidInput = true; 
    
    do
    {
      System.out.println("Please enter the " + i + " digit of your combo lock (between 1-3)?");
      numStr = input.nextLine();
      
      errMsg = "Sorry, \" " + numStr + " \" is not an integer\n";
      
      try
      {
        num = Integer.parseInt(numStr); // Convert the number from a String to an double
        
        if (num < 1 || num > 3)
        {
          num = Integer.parseInt("Error");
        }
        
        notValidInput = false;
      }                              
      catch (NumberFormatException error)  
      {
        System.out.println(errMsg);
      }
      
    }while(notValidInput);  // As long as input is a negative, repeat
    
    return num;
  }
  public static void simulateUnlockAttempt(ComboLockIshP comboLock,int[] combo)
  {
    boolean isUnlocked = false;
    int[] checkCombo = new int[3];
    
    for (int i = 0; i < 3; i++) 
    {
      System.out.println("\nAttempt "+ (i+1) + " to Open Lock");
      
      checkCombo = getCheckCombo(checkCombo);
      
      isUnlocked = comboLock.unlock(checkCombo);
      
      if (isUnlocked == true)
      {
        break;
      }
    }
    
    if (isUnlocked == false)
    {    
      System.out.println("You have failed to open the lock after 3 tries.");
      System.out.println(comboLock);                  
    }
  }
  public static int getOptionToRepeat()
  {
    Scanner input = new Scanner(System.in);
    String numStr = "", errMsg;
    int num = 0;
    boolean notValidInput = true; 
    
    do
    {
      System.out.println("\nWould you like to repeat the Lock Simulation \nYou can \n[Repeat the Simulation: 1]\n[End the Program: 2]");
      numStr = input.nextLine();
      
      errMsg = "Sorry, \" " + numStr + " \" is not an integer between 1 to 2\n";
      
      try
      {
        num = Integer.parseInt(numStr); // Convert the number from a String to an double
        
        if (num < 1 || num > 2)
        {
          num = Integer.parseInt("Error");
        }
        
        notValidInput = false;
      }                              
      catch (NumberFormatException error)  
      {
        System.out.println(errMsg);
      }
      
    }while(notValidInput);  // As long as input is a negative, repeat
    
    return num;
  } 
  public static int[] getCheckCombo(int[] checkCombo)
  {
    int counter = 0;
   
    for (int k = 0; k < checkCombo.length; k++) 
    {
      counter = k+1;
      checkCombo[k] = getSingleDigit(counter);
    }
    
    return checkCombo;
  } 
}