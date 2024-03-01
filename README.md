# Summary:
We have been given a PDF with information about an insurance applicant.
We are tasked with leveraging OpenAI and Retrieval-Augmented Generation (RAG) to review the application and give an informed recommendation as to whether or not a company should provide insurance to this person.


# Assumptions:


*   The provided application is for life insurance.
*   While document interpretation should not be overfit to this particular example, it is likely that future applications will follow similar patterns.
*   This is whole life insurance and the **premiums do not change**. Premiums and other pricing considerations could be easily modified in future versions.
*   Approval should be granted when the company can be reasonably sure that they will not lose money on the policy.
*   The company will not lose money if the combination of applicant payments + modest interest returns on the cumulative payments is greater than the payout amount of the policy after n_years.
*   If accepted, the applicant will pay for the policy for the lesser of: their remaining lifetime or 100 years. Future versions apply additional predicted information leveraging attrition/churn modeling.
*   For the purposes of this exercise, the total amount paid by the applicant is equal to n_years * annual_premium, though future versions could be adapted to respond to different payment plans.


# Approach:


1.   Collect basic demographic information about the individual (age, sex)
2.   Parse the document for additional information about the individual's health and habits in order to determine an appropriate risk class
3.   Using this information and guesstimated weights, calculate the risk score and assign a risk class of premium, standard, or sub-standard to the individual
4.   With the individual's age, sex and risk class, leverage Pandas agents to lookup pre-loaded and processed data to answer the following:

*   **Question 1**: Is the applicant likely to pay an amount ≥ $250,000?

>*   **If no:** The company should reject the applicant.

>*   **If yes:** The company should find the greatest amount of insurance for which the applicant would be eligible.

*   **Question 2**:
For eligible applicants, what is the probability that they pay an amount ≥ each eligible tier of insurance?

# Outcome:
Provide the user with a summary of eligibility and final recommendations.



#Assets and Artifacts:

*   **[Billing codes](https://www.surgery.northwestern.edu/docs/cpt-codes.pdf):** Accessed via web 02.27.2024. Unmodified. Referenced via RAG.

*   **[Code Costs](https://www.cms.gov/research-statistics-data-and-systems/statistics-trends-and-reports/medicarefeeforsvcpartsab/downloads/level1charg13.pdf):** Accessed via web 02.27.2024. Slight modification and augmentation. Ultimately not leveraged in final solution.

*   **[Actuarial tables](https://www.ssa.gov/oact/STATS/table4c6.html):** Accessed via web 02.27.2024. Processing and augmentation applied. Referenced via Pandas agent.

*   **[Sample Policy Costs](https://www.policygenius.com/life-insurance/):** Accessed via web 02.27.2024. Heavily augmented via interpolation and extrapolation for use as sample data. Referenced via Pandas agent.

*   **[Sample Application]("/content/fake-aps.pdf"):** Provided as part of challenge. Unmodified. Referenced via RAG.

