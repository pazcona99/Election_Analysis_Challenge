# Election_Analysis_Challenge

Working analysis of a Colorado election to assess the winner as well other statistics of the vote.

---

# Overview of Election Audit: 

There was a time when the election audits were tallied by hand. However, with the advent of the computer processor, such a menial and tedious task can be automated. If presented with the right, quality-assured data it would be possible to write a script that can assess an election cycle's result in less than a second. 

In this scenario, the working data consisted of a Colorado congressional seating election cycle. The purpose of this anaylsis was to visualize the amount of votes received per candidate and county, and then realize the winning candidate of the cycle. The data consists of 369,711 rows of voter information for which a script iterates and attains summation values.

---

# Election-Audit Results: 
The following list will address the election outcomes. 

1. How many votes were cast in this congressional election?
   - The number of votes cast was 369,711. This number is the totality of all voters across three counties including Denver, Jefferson, and Arapahoe.
   - The code for this calculation was created by establishing a counter that is run iteratively within a `for` loop. Essentially, for each row that's counted, the variable for total votes adds 1 to itself. This code is would be as shown below.

         for row in reader:

            # Add to the total vote count
            total_votes = total_votes + 1

        
2. Provide a breakdown of the number of votes and the percentage of total votes for each county in the precinct.
   - The number of votes can be broken down further by evaluating the total votes for each candidate. The results are shown below:
     - Charles Casper Stockham: 23.0% (85,213)
     - Diana DeGette: 73.8% (272,892)
     - Raymon Anthony Doane: 3.1% (11,606)
     
     Similarly to the total votes counter, the number of votes for each voter can be found by extracting a candidate's name from each of the rows. All the rows are evaluated to find a unique name associated with candidates such that all candidate's are accounted for and listed. From this list of candidate options, and for each row, the vote count is increased by 1 within a dictionary. This code would look like that below:

            if candidate_name not in candidate_options:

                  # Add the candidate name to the candidate list.
                  candidate_options.append(candidate_name)

                  # And begin tracking that candidate's voter count.
                  candidate_votes[candidate_name] = 0

            # Add a vote to that candidate's count
            candidate_votes[candidate_name] += 1


   - The number of votes can be broken down further by evaluating the total votes for each county. The results are shown below:
     - Jefferson: 10.5% (38,855)
     - Denver: 82.8% (306,055)
     - Arapahoe: 6.7% (24,801)

     Similarly to the total votes counter, the number of votes for each county can be found by extracting a county's name from each of the rows. All the rows are evaluated to find a unique string associated with row such that all counties are accounted for and listed. From this list of counties, and for each row, the vote count is increased by 1 within a dictionary. This code would look like that below:

            if county_name not in county_list:

                     # Add the existing county to the list of counties.
                     county_list.append(county_name)

                     # Begin tracking the county's vote count.
                     county_votes[county_name] = 0

                  # Add a vote to that county's vote count.
                  county_votes[county_name] += 1

3. Which county had the largest number of votes?
   - The county with the largest number of votes is Denver. Denver was the county that accounted for approximately 82% of the vote. 

   This result was determined within the code through a conditional statement that evaluates from the winnning county and gets its vote. This lives within a `for` loop that checks for each county name from a county dictionary. The code would look like the below: 

        if (votes_in_county > xlcounty_turnout_votes) and (votes_in_county_percent > xlcounty_turnout_votes_percent):
                    xlcounty_turnout_votes = votes_in_county
                    xlcounty_turnout = county_name

4. Provide a breakdown of the number of votes and the percentage of the total votes each candidate received.
   - With resepct to the percentage for each candidate, the winner was quite clear in Diana DeGette by receiving 73.8% of the total vote. This value, for each candidate, was assessed by extracting the vote count for each candidate from it's respective dictionary, and then dividing this value by the total vote.

   The code would look like that shown below:

        votes = candidate_votes.get(candidate_name)
        vote_percentage = float(votes) / float(total_votes) * 100

5. Which candidate won the election, what was their vote count, and what was their percentage of the total votes?
   - As stated above, the winner clearly was Diana Degette. However, to be sure, and to output the winner automatically there is a script that was written to print this information.  

    In order to realize the winning candidate, a conditional `if` statement was written to check if the first vote count for a candidate is greater than zero. If the statement is true, then that vote count will be equal to the "winning count." Then the candidate as the "winning candidate" from the candidate_options list will be printed along with their count and percentage. A code for this would look like the below:

        if (votes > winning_count) and (vote_percentage > winning_percentage):
                winning_count = votes
                winning_candidate = candidate_name
                winning_percentage = vote_percentage

---

# Election-Audit Summary: 

The election of Colorado is only a small subset of data, but it can be said that it can be applied to the entirety of the state and perhaps even the entirety of the United States. This script has the ability to take thousands of lines of voter data, and print the winner in a fraction of the time. This is of course assuming the correct, quality assured data has been provided for the analysis.

The code can be modified further as a refinement to the election process. One example for modifying the code is to expand the capability of it so that it can assess beyond the counties that it is provided. This would require some additional data; however, the counties can all be associated with a state. The counties and their respective votes can live as a value within a state dictionary for which the name of the state is the key. The code would be modified similar to the county conditional statement to include both a list and a dictionary for the counties and the state.  These two entities can be tracked on separate lines of code that then can be merged at the end prior to printing. The ouput of this script can include the number of votes cast within that state, and in each county, and also determine the winner at the state level by the popular vote.

Another idea for expanding the limits of this code include not only by finding the winner based on popular vote or the number of votes per county, but it would be a good metric to know the performance of each candidate per county. Could it be possible that Diana faired better in the county of Denver alone and lost in Jefferson? This can provide a useful insight to the election cycle that can be used for future elections. This modification to the code would include creating an additional list that for each county and for each particular candidate name found in a row an addition counter value is added. This will ensure that every time the name is found in a particular county it adds to itself as a vote. The output would be each county and the number of votes each candidate received in that district, and it could be taken a step further by printing the winner for that particular county as well based on a conditional statement for finding the greatest value of votes.

There was a time where knowing this information took hours of counting and analyzing voter information towards the particular statistic. But with the right code, this is something that can be done effortlessly every election cycle.
