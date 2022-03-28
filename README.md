# An Analysis of Election Results

## Project Overview

### I will be assisting the Colorado Board of Elections with an audit of the election results for a U.S. Congressional Precinct in Colorado.

## Analysis

Through the use of Python and csv and os dependencies, I was able to determine how many votes were cast in total, as well as how many for each candidate. Furthermore, I was then able to determine the voter turnouts in each county. The first step was to load the dependencies needed, at which point I accessed the csv file with the election data:

    import csv
    import os

    file_to_load = os.path.join("Resources", "election_results.csv")

Once the file data was accessed I converted it to a list of dictionaries that I was then able to analyze. I used the reader function followed by a for loop to loop through the rows, tallying the votes with each row. I also captured the candidate and county names in corresponding variables. I then nested an if statement that added any candidate names and county names that were not in the corresponding lists. This allowed me to create complete lists of all candidates and counties. After their respective if statements, I added a vote to the tally for the corresponding candidate and county. The code for all of this can be seen below:

    with open(file_to_load) as election_data:
      reader = csv.reader(election_data)

      header = next(reader)

      for row in reader:

        total_votes = total_votes + 1

        candidate_name = row[2]

        county_name = row[1]

        if candidate_name not in candidate_options:

            candidate_options.append(candidate_name)

            candidate_votes[candidate_name] = 0

        candidate_votes[candidate_name] += 1

        if county_name not in county_list:

            county_list.append(county_name)

            county_votes[county_name] = 0

        county_votes[county_name] += 1

Now that I had all of the votes tallied for candidates and counties, I could carry out the simple calculations needed to determine percentages. I could also determine the winner of the election, and the county with the highest voter turnout. I used both the print function and the write function, so that the results were printed to the terminal screen and written to a txt file. Here is a small example of the code used to write and print the results:

    file_to_save = os.path.join("analysis", "election_analysis.txt")
    
    with open(file_to_save, "w") as txt_file:

      election_results = (
        f"\nElection Results\n"
        f"-------------------------\n"
        f"Total Votes: {total_votes:,}\n"
        f"-------------------------\n\n"
        f"County Votes:\n")
      print(election_results, end="")

      txt_file.write(election_results)
      
## Results

The final results of my analysis as shown on my terminal screen are as follows:

![Election Results](https://github.com/NickBaldassarre/Election_Analysis/blob/4ab06405b14fc907a35908690145573e4689396f/Resources/election_results.png)

* The total number of votes cast in this election were 369,711
* Arapahoe had 6.7% of the votes with 24,801, Jefferson had 10.5% of the votes with 38,855, and Denver had 82.8% of the votes with 306,055.
* Denver clearly had the largest number of votes.
* Raymon Doane received 3.1% of the votes with 11,606, Charles Stockam receivec 23% of the votes with 85,213, and Diana DeGette received 73.8% of the votes with 272,892.
* Diana DeGette was the clear winner of this election with 306,055 votes cast for her; a landslide 73.8% of the vote!

## Summary

The code used for this analysis is very versatile and can be applied to any number of elections in the future. So long as the election data is compiled in a clean csv file, minor modifications to this code could be employed to analyze it. One example of a modification would be if we were looking at an entire country, we would add lists and dictionaries for states in addition to counties and candidates:

    state_list = []
    state_votes = {}
    
We could then use the same type of membership if statements used in this analysis to populate the list and dictionary. 

Another modification that could be applied would be to analyze the results by county, which would give even more perspective on who voters were supporting in different areas. To do this, we could write a nested for loop that uses membership if statements to create new dictionaries for the results of each county. There are many possibilities for where we could take this.
