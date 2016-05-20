/* A program to create a population and 
 then find the year with the most people alive
 Author: Chris DeDear */
 
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Scientific
{
    // Person Object with birth and death year
    class Person
    {
        int yearBorn=0;
        int yearDied=0;       
        
        // Constructor
        public Person(int born, int died)
        {
            yearBorn = born;
            yearDied = died;         
        }
        // Getters
        public int YearBorn { get { return yearBorn; } }
        public int YearDied { get { return yearDied; } }
       
        public void Output()
        {
            Console.WriteLine(yearBorn + " - " + yearDied );
        }
    }
    class Program
    {
        // Const Ints used for restraints
        const int MIN_YEAR = 1900;
        const int MAX_YEAR = 2000;
        // Main 
        static void Main(string[] args)
        {
            // Set the variables to be used to display the correct info
            int MaxAlive = 0;
            int MaxYear = 0;
            // Set up the dataset with the appropriate ammount of items
            Person[] persons = new Person[250];
           
            // Run the function to populate the dataset with random data
            SetPopulation(persons);
            // Array used to span the years 1900 to 2000
            int[] years = new int[101];
            // Loop through each person in the Persons array
            for (int nPersonIt = 0; nPersonIt < persons.Length; nPersonIt++)
            {
                // Increment each year that he person object is alive inclusive of the death year
                for (int j = persons[nPersonIt].YearBorn - MIN_YEAR; j <= persons[nPersonIt].YearDied - MIN_YEAR; j++)
                {
                    years[j]++;
                }
            }
            // Iterate through year array to set MaxAlive, MaxYear and outut yearly info
            for (int nYearIt = 0; nYearIt < years.Length; ++nYearIt)
            {
                Console.WriteLine("year " + (MIN_YEAR + nYearIt) + "; Amount alive: " + years[nYearIt]);
                if(years[nYearIt] > MaxAlive)
                {
                    MaxAlive = years[nYearIt];
                    MaxYear = MIN_YEAR + nYearIt;
                }
            }
            // Output the correct info
            Console.WriteLine("The year with the max people alive is: " + MaxYear + " with " + MaxAlive + " people alive.");  
        }
        // Sets the populations dataset
        public static void SetPopulation(Person[] array)
        {
            Random r = new Random();
            int born = 0;
            for (int i = 0; i< array.Length; ++i)
            {
                // Set the year born between the 2 restraints
                born = r.Next(MIN_YEAR, MAX_YEAR +1);
               
                // Set the person object to the array
                array[i] = new Person(born, r.Next(born, MAX_YEAR + 1));     
                // Output the persons data for verification
                array[i].Output();
            }
        }
    }
}
