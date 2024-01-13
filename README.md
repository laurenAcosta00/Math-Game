# Math-Game
 This Java program is a simple random number generator game with a menu-driven interface. 
import java.util.Arrays;
import java.util.Scanner;
import java.util.Random;
//Name Lauren Acosta
//Date 9/5/2022


public class mathGame {


	// method for generating random array values 
	public static void getRandomNumber(int A[],int n)
	{
		//n random values stored in an integer array 
		Random generator = new Random();
		int nextRand;

		// iterates through n number of elements in array 
		for(int i=0;i<n;i++)
		{
			//The range of random numbers are between 5 and 20.
			nextRand = 5+generator.nextInt(20);
			A[i]=nextRand;
		}

	}


	// method for printing out updated array throughout program 
	public static void printArray(int[] A)
	{

		for (int i=0; i<A.length; i++) 
		{
			System.out.printf("%d ", A[i]);
		}
		System.out.println();
	}


	// method for 1st menu option, play game 
	public static void playGame(int[] A,int n)
	{

		Scanner userInput = new Scanner(System.in);
		int scan;

		// getting random set of values from print array method 
		System.out.println("Add these values:");
		printArray(A);
		scan= userInput.nextInt();

		int realSum = actualSum(A,n);

		// if user input equals the calculated sum value 
		if(compare(realSum, scan) == true) 
		{
			System.out.println("That is correct!\n");

		}
		// if user input does not equal calculated sum value 
		else
		{
			System.out.println("That was incorrect. The value adds to be: " + realSum + "\n");
		}


	}


	// boolean method for comparing user input and calculated answer for playGame method 
	public static boolean compare(int actualSum, int userSum)
	{
		if(userSum == actualSum)
		{
			return true;
		}
		return false;

	}

	// method for obtaining the sum of random values for playGame method 
	public static int actualSum(int[] A, int n)
	{
		int sum =0;


		for(int i=0; i<n; i++)
		{
			sum += A[i];

		}
		return sum;
	}


	// method for each shuffle, randomly select two values and switch their values in the array.
	public static void shuffle(int[] A, int n)
	{

		Scanner input = new Scanner(System.in); 

		int userSwaps=0;

		System.out.print("Current: ");
		printArray(A);

		System.out.println("How many swaps?");
		userSwaps= input.nextInt(); 

		// performing the actual swap 
		for(int i=0; i<userSwaps;i++)
		{
			int temp1= generatePos(n);
			int temp2= generatePos(n);
			// final state of the array after swap 
			swap(A,temp1,temp2);
		}

		System.out.print("Final: ");
		printArray(A);
		System.out.print("\n");
	}


	// method to perform shuffle, used in shuffle method 
	public static void swap(int []A, int pos1, int pos2)
	{
		int temp= A[pos1];
		A[pos1]= A[pos2];
		A[pos2]= temp;


	}


	// method for randomly selecting positions in array, used in shuffle method 
	public static int generatePos(int n)
	{
		//n random values stored in an integer array 
		Random generator = new Random();

		return 0+generator.nextInt(n);
	}

	// method for option 3 of menu. generates new numbers, reassign all values in the current array
	public static void newValues(int []A, int n)
	{
		Random generator = new Random();

		// iterates through n number of elements in array 
		for(int i=0; i<n; i++)
		{
			//Ranges should be 5-20
			A[i]= 5+generator.nextInt(20);
		}
		System.out.print("New Values: ");
		printArray(A);
		System.out.print("\n");
	}






	public static void main(String[] args) {

		Scanner scan = new Scanner(System.in);

		//User will put in an integer valued from 2 - 25.  I will call this variable n. 
		int n; 

		System.out.println("Welcome to random number generator!");
		System.out.println("How many values would you like to use:");
		n = scan.nextInt();

		//randomly populated array with n number of elements selected by user input 
		int[] A = new int[n];
		getRandomNumber(A, n);

		System.out.println("Created!");

		// while loop to simultaneously run the menu options 
		while(true)
		{

			Scanner input = new Scanner(System.in);
			int choice =0;

			System.out.println("Select your option:");
			System.out.println("1. Play Game");
			System.out.println("2. Swap Values");
			System.out.println("3. New Values");
			System.out.println("4. Sort");
			System.out.println("5. Exit");

			choice = scan.nextInt(); 

			// calling the methods accordingly to user/menu options 
			if(choice==1)
			{
				playGame(A,n);
			}
			if(choice==2)
			{
				shuffle(A,n);
			}
			if(choice==3)
			{
				newValues(A,n);
			}
			if(choice == 4) 
			{
				//option 4, calls printArray function since its implemented with random values already 
				System.out.print("Current: ");
				printArray(A);

				// use built in sort function to sort current array and then print its final state 
				System.out.print("Final: ");
				Arrays.sort(A);
				printArray(A);
				System.out.print("\n");
			}
			if(choice == 5) 
			{
				//end the loop
				System.out.print("Goodbye");
				return;
			}

		}
	}

}
