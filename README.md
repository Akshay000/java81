class DefinedException {
 
    public static void main(String args[]) 
	{
        Account acct = new Account();
        System.out.println("Current balance : " + acct.balance());
        System.out.println("Withdrawing $200");
        acct.withdraw(2000);
        System.out.println("Current balance : " + acct.balance());
        acct.withdraw(10000);
 
    }
 
}
 
class Account 
{
 
    int balance = 10000;
    int balance() 
	{
        return balance;
    }
 
    public void withdraw(int amount) throws NotSufficientFundException 
	{
        if (amount > balance) 
		{
            throw new NotSufficientFundException(String.format("Current balance %d is less than requested amount %d", balance, amount));
        }
        balance = balance - amount;
    }
 
    public void deposit(int amount) 
	{
        if (amount <= 0) 
		{
            throw new IllegalArgumentException(String.format("Invalid deposit amount %s", amount));
        }
    }
 
}

class NotSufficientFundException extends RuntimeException 
{ 
       String message;
	
       NotSufficientFundException(String message) 
	{
        this.message = message;
    }
 
      NotSufficientFundException(Throwable cause, String message) 
	{
        super(cause);
        this.message = message;
    }
 
     String getMessage() 
	{
        return message;
    }

}


Output:
       Current balance : 10000
       Withdrawing $2000
       Current balance : 8000
       Exception in thread "main" NotSufficientFundException: Current balance 8000 is less than requested amount 10000
               at Account.withdraw(Testing.java:68)
               at Testing.main(Testing.java:51)
