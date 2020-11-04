# weather-generator-java
public class WeatherGenerator { 

    /* Given a location (longitude, latitude) in the USA and a month of the year, the method
     * returns the forecast for the month based on the drywet and wetwet transition 
     * probabilities tables.
     * 
     * month will be a value between 2 and 13: 2 corresponds to January, 3 corresponds to February
     * and so on. These are the column indexes of each month in the transition probabilities tables.
     * 
     * The first day of the month has a 50% chance to be a wet day, 0-0.49 (wet), 0.50-0.99 (dry)
     *
     * Use StdRandom.uniform() to generate a real number uniformly in [0,1)
     */
     int[] oneMonthGenerator(double longitute, double latitude, int month, double[][] drywet, double[][] wetwet)

     // Returns the longest number of consecutive mode (WET or DRY) days in forecast.
     int numberOfWetDryDays (int[] forecast, int mode)

    /*
     * Analyzes the forecast array and returns the longest number of 
     * consecutive mode (which can be WET or DRY) days in forecast.
     */
     int lengthOfLongestWetDrySpell (int[] forecast, int mode)
}
java WeatherGenerator111 -98.76 26.70 3
public static void main (String[] args) {

        int numberOfRows    = 4001; // Total number of locations
        int numberOfColumns = 14;   // Total number of 14 columns in file 
                                    // File format: longitude, latitude, 12 months of transition probabilities
        
        // Allocate and populate arrays that hold the transition probabilities
        double[][] drywet = new double[numberOfRows][numberOfColumns];
        double[][] wetwet = new double[numberOfRows][numberOfColumns];
        populateTransitionProbabilitiesArrays(drywet, wetwet, numberOfRows);

        /*** WRITE YOUR CODE BELLOW THIS LINE. DO NOT erase any of the lines above. ***/

        // Read command line inputs 
        double longitute = Double.parseDouble(args[0]);
        double latitude  = Double.parseDouble(args[1]);
        int    month     = Integer.parseInt(args[2]);

        int[] forecast = oneMonthGenerator(longitute, latitude, month, drywet, wetwet);
        int drySpell = lengthOfLongestSpell(forecast, DRY);
        int wetSpell = lengthOfLongestSpell(forecast, WET);

        StdOut.println("There are " + forecast.length + " days in the forecast for month " + month);
        StdOut.println(drySpell + " days of dry spell.");

        for ( int i = 0; i < forecast.length; i++ ) {

            // This is the ternary operator. (conditional) ? executed if true : executed if false
            String weather = (forecast[i] == WET) ? "Wet" : "Dry";  
            StdOut.println("Day " + (i+1) + " is forecasted to be " + weather);
        }
    }
