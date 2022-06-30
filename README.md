# Election Analysis
Analyze election results using Python
## Overview of Election-Audit
After developing the code to analyze election results for a group of candidates, I expanded upon its functionality to analyze results by county. For candidates, this detailed analysis tallied the total number of votes in the given election, the total number of votes each candidate recieved alongside the percentage of votes they recieved, and displayed which among the candidates had won along with their statistics. For counties, this analysis tallied the total number of votes submitted by each county and their percentage of the total vote. After the statistics for each county had been tallied, the county with the largest voter turnout is displayed. Finally, all of the analyses were compiled into a text file for easy transmission and readability.
## Election-Audit Results
In order to track the results of this election, I would need a variety of variables to store data as the election csv was being processed. To store the total votes tracked in this election, I needed a "total_votes" variable initialized as an integer. To track candidates that in the csv file and to track their votes, I created a "candidate_options" list and a "candidate_votes" dictionary. Similarly, a "county_list" list and a "county_votes" dictionary were used to track the results for each county. For the results of the election, a "winning_candidate" string, a "winning count" integer, a "winning_percentage" float, a "largest_county" string, and a "largest_votes" integer were all initialized to store my analysis.

For ease of access, the paths to the csv file that contained the election data and the txt file that would store my analysis were stored as follows:

`file_to_load = os.path.join("..", "Resources", "election_results.csv")`

`file_to_save = os.path.join("analysis", "election_analysis.txt")`

With all of these variables initialized and the paths stored, I was ready to begin my analysis. First, the csv file neede to be opened to read.

`with open(file_to_load) as election_data:`

`reader = csv.reader(election_data)`

Next, the header needed to be processed:

`header = next(reader)`

To loop through each row of data, a for loop was necessary: 

`for row in reader:`

At each of this loop's itterations, the "total_votes" would need to be incremented as such:

`total_votes = total_votes + 1`

Additionally, the candidate name and county name would need to be extracted from each vote:

`candidate_name = row[2]`

`county_name = row[1]`

If the candidate's name was not already stored in the "candidate_options" list, then this name would need to be appended and its corresponding "candidate_votes" would need to be initialized to 0:

`if candidate_name not in candidate_options:`

`    candidate_options.append(candidate_name)`

`    candidate_votes[candidate_name] = 0`

After this check, the candidate's vote count is incremented by 1 to track the vote:

`candidate_votes[candidate_name] += 1`

Similarly, if the county's name was not already stored in the "county_list", then this name would need to be appended and its corresponding "county_votes" would need to be initialized to 0:

`if county_name not in county_list:`

`    county_list.append(county_name)`

`    county_votes[county_name] = 0`

After this check, the county's vote count is incremented by 1 to track the vote:

`county_votes[county_name] += 1`

With the data from the csv completely read through, the txt file needed to be opened to store the processed analysis I was creating:

`with open(file_to_save, "w") as txt_file:`

Both printed in the program and written in the txt file, I would then set up the header of my output, display the total votes, and prepare the display for the votes of each county:

`election_results = (`

`    f"\nElection Results\n"`

`    f"-------------------------\n"`

`    f"Total Votes: {total_votes:,}\n"`

`    f"-------------------------\n"`

`    f"County Votes:\n")`

`print(election_results, end="")`

`txt_file.write(election_results)`

Next, I would need to loop through each county utilizing the following for loop:

`for county in county_votes:`

For each of the counties, I stored the vote count of the county, calculated the percentage of total votes this made up, print this result, and write it to the txt file:

`votes = county_votes.get(county)`

`percentage_votes = float(votes) / float(total_votes) * 100`

`county_result = (f"{county}: {percentage_votes:.1f}% ({votes:,})\n")`

`print(county_result)`

`txt_file.write(county_result)`

Also within this for loop, I needed to check to see if the current county had the highest vote count. If this county had the highest vote count, the county name and number of votes would need to be stored in the "largest_county" and "largest_votes" variables:

`if county_votes.get(county) > largest_votes:`

`    largest_county = county`

`    largest_votes = county_votes.get(county)`

After looping through each of the counties, the county witht he largest number of votes would need to be displayed and written in the txt file:

`largest_result = (`

`    f"-------------------------\n"`

`    f"Largest County Turnout: {largest_county}\n"`

`    f"-------------------------\n")`

`print(largest_result)`

`txt_file.write(largest_result)`

Following the same format as the counties loop, the candidates were looped through to determine the candidate with the most votes and their corresponding vote percentage and to print store them in the txt file.

The result of this analysis was the followning text file:

![Election Results](https://github.com/waciciarelli/Election_Analysis/blob/main/challenge/Resources/Election%20Analysis%20Results.png?raw=true)

## Election-Audit Summary
By utilizing this analysis tool, any election can be analyzed in a similar fashion. All that would need to be changed to make this more universal would be to alter the path of the file to read to a new csv file. This analysis is a great start to an analysis of voters within specific areas. However, there is still room for it to be improved. For example, rather than having the path to the csv file be set by being coded in by the developer, this could be changed to take input from the user to create a custom path towards the intended file. Additionally, this type of analysis would benefit greatly from analyzing by political party. An political party analysis similar to the county analysis would provide much vital information on the political views during a particular election. Furthermore, these analyses can be combined into a political party analysis by county to geographically locate particular political parties.
