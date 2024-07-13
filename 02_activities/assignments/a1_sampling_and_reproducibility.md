# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 1000 (from the original 50000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: MAMDOUH ZAYDAN (ALL CODES ARE IN assignment-1.ipnyb)



# ANSWER PART 1:
1) Sampling Stages Identified in the Model:  

1-1) Primary Infection Simulation:  
Procedure: Randomly selects a subset of individuals to infect based on ATTACK_RATE.  
Function Used: np.random.choice().  
Sample Size: Proportional to ATTACK_RATE and the total number of individuals.  
Sampling Frame: Entire population attending weddings and brunches (ppl DataFrame).  
Underlying Distribution: Uniform distribution (np.random.choice()).  
  
  
1-2) Primary Contact Tracing:  
Procedure: Determines which infected individuals are traced based on TRACE_SUCCESS.  
Function Used: np.random.rand() for probability comparison.  
Sampling Frame: Infected individuals (ppl['infected']).  
Underlying Distribution: Uniform distribution (np.random.rand()).  
  
1-3)Secondary Contact Tracing:  
Procedure: Extends tracing to individuals who attended events with a certain threshold of traces (SECONDARY_TRACE_THRESHOLD).  
Function Used: Boolean indexing with value_counts() to identify events meeting the threshold.  
Sampling Frame: Traced individuals (ppl[ppl['traced'] == True]).  
Underlying Distribution: Boolean condition (threshold check).  



2) Description of Sampling Procedures:

2-1) Primary Infection Simulation:
Simulates initial infections across event attendees.
np.random.choice() randomly selects individuals to be infected based on ATTACK_RATE.

2-2) Primary Contact Tracing:
Determines which infected individuals are traced based on TRACE_SUCCESS.
np.random.rand() generates probabilities to decide tracing outcomes.


2-3) Secondary Contact Tracing:
Expands tracing to individuals who attended events with a significant number of traces (SECONDARY_TRACE_THRESHOLD).
Uses value_counts() and boolean indexing to identify and trace further individuals.
  
  
  
3) Relation to the Blog Post:  
The sampling procedures in the script simulate biases discussed in the blog post related to contact tracing.  
They illustrate how selective sampling of infected and traced individuals can influence perceived infection sources (e.g., weddings vs. brunches).


# ANSWER PART 2:
It seems that a significant number of COVID are traced back to weddings in the proportion 15% to 26% and peak in the range 13%-22%.  

It seems that a significant number of infections originate from weddings especially in ranges of 13%-25%.  

This shows a higher proportion of both traced cases and infection from weddings which aligns with the potential biases discussed in the article of Andrew Whitby.

# ANSWER PART 3:

Comment on Reproducibility of Simulation Results:

After running the simulation code multiple times and generating three separate images containing histograms of "Infections from Weddings" and "Traced to Weddings," it's notable that the histograms appear consistent across all runs. This indicates a high degree of reproducibility in our simulation results.

Observations:

The histograms for both "Infections from Weddings" and "Traced to Weddings" show similar distributions and patterns across different runs.
The proportions of infections and traced cases attributed to weddings exhibit minimal variation, suggesting that the simulation outcomes are stable and predictable under the given parameters.
Factors Contributing to Reproducibility:

Random Seed Consistency: The use of a fixed random seed (set to 10 in our case) ensures that each simulation run produces deterministic results. This consistency in random number generation helps in comparing results across different runs.
Stochastic Elements: Despite the stochastic nature of infection spread and contact tracing mechanisms, the overall trends in the histograms remain unchanged. This indicates that the simulation captures robust patterns that are not heavily influenced by random fluctuations.


# ANSWER PART 4:

The code modifications involved increasing the number of simulation repetitions from 1000 to 60000 by adjusting the range parameter in the simulate_event function. Additionally, I ensured reproducibility by setting a fixed random seed (np.random.seed(10+m)) before running the simulations. These changes enhanced reproducibility by maintaining consistency in random number generation across different script executions, ensuring that the results remain stable and comparable each time the script is run.



## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `HH:MM AM/PM - DD/MM/YYYY`
* The branch name for your repo should be: `sampling-and-reproducibility`
* What to submit for this assignment:
    * This markdown file (sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `sampling-and-reproducibility`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-3-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
