package ComboLockDriver;

public class ComboLockIshP 
{
  private int[] combination;
  
  public void setLock(int[] combo)
  {
    combination=combo;
  }
  public boolean unlock(int[] checkCombo)
  {
    if(combination[0] == checkCombo[0] && combination[1] == checkCombo[1] && combination[2] == checkCombo[2])
    {
      System.out.println("\n                      Nice you have Opened the Lock!                           ");
      System.out.println("---------------------------------------------------------------------------------");
      return true;
    }
    else
    {
      System.out.println("\n                   Your Attempt to open the Lock Failed                         ");
      System.out.println("----------------------------------------------------------------------------------");
      return false;
    }
  }
  public String toString() 
  {
    String output = "The Lock Combination was: "+combination[0]+combination[1]+combination[2];
    return output;
  }
}