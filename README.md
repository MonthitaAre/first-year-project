# Does the presence of a stable working group in any way affect the outcome of the case and punishment?

This project aims to explore the impact of having a stable working group on the outcomes of criminal cases and the severity of punishments handed down under Article 105, "Murder," of the Criminal Code of the Russian Federation. The dataset used for this analysis consists of case cards and texts of court decisions collected directly from 2,231 federal general jurisdiction court websites, covering the period from 2016 to 2023.

Due to computational limitations, the full dataset is too large to process in its entirety for this analysis. Therefore, this project focuses on a subset of the original dataset, specifically the data for the year 2017.


The dataset contains the following columns, detailed in the accompanying .csv file:
| №  | Feature      | Description                                                                 |
|----|--------------|-----------------------------------------------------------------------------|
| 1  | id           | Case identifier within the dataset                                          |
| 2  | region       | Region number in the Justice Integrated Automated System                    |
| 3  | year         | Year                                                                        |
| 4  | instance     | Instance: FIRST — first instance; APPELLATION — appellation instance.       |
| 5  | court_name   | Court name                                                                  |
| 6  | caseNumber   | Case number within the court                                                |
| 7  | entryDate    | Date of case filing in court                                                |
| 8  | names        | Names of the accused and articles of the criminal code under which the charges were brought |
| 9  | judge        | Judge                                                                       |
| 10 | resultDate   | Date of case consideration                                                  |
| 11 | decision     | Verdict. Courts in regions use different wordings.                          |
| 12 | endDate      | Date of case completion                                                     |
| 13 | consideredBy | Признак рассмотрения дела (кем рассмотрено).                                |
| 14 | cui          | Unique case identifier used by courts to link cases across different instances. In some court case cards, the unique identifier is missing. |
| 15 | accused      | Names of the accused                                                        |
| 16 | hash         | Hash for names of the accused                                               |
| 17 | articles     | Composition of charges (articles of the criminal code under which the charges were brought). If there were multiple defendants in the case, all articles for each defendant are listed. |
| 18 | link_meta    | Link to the court case card. For some courts, the direct link may not work as these courts use CAPTCHA. |
| 19 | link_text    | Link to the text of the court decision                                      |
| 20 | is_text      | Indication of the availability of the text of the court decision            |
| 21 | text         | Text of the court decision, if it was available in the court case card on the court's website. |

The concept of stable working groups in courtrooms involves the same judge, prosecutor, and defense attorney collaborating on multiple cases. Extensively studied in the US by researchers like Eisenstein and Jacob (1977) and Nardulli (1978), these groups develop shared norms and cooperative techniques, influencing court decisions.

In Russia, stable working groups are identified by recurring combinations of legal professionals handling many cases together over time. This can lead to more predictable and potentially more severe judicial decisions.

Regular interactions among the same judge, prosecutor, and defense attorney can streamline the trial process and enhance case management through familiarity with each other's styles (Eisenstein & Jacob, 1977; Nardulli, 1978). However, this can also introduce bias. Close relationships between judges and prosecutors may lead to favoritism or harsher sentencing for defendants (Haynes et al., 2010). While stable working groups may increase efficiency and consistency, they can also result in uniform and sometimes stricter sentencing practices (Johnson, 2006).

To investigate whether stable working groups affect the outcomes and severity of punishments in Russian courts, I conducted an empirical analysis using court decision data from 2017. The analysis involved data extraction, preprocessing, and applying machine learning models to evaluate the influence of these stable working groups.

**1. Data Collection**

I utilize the 'text' column to extract information about the judges, prosecutors, and defense attorneys involved in each case, along with the case outcomes and the severity of punishments.

The key variables in our study include:

**Independent Variable:**
  - Stable Working Groups: Identifies instances where the same judge, prosecutor, and defense attorney work together on a case.

**Dependent Variables:**
  - Judicial Outcomes: A binary variable indicating whether the defendant was found guilty or not guilty. We'll analyze if stable working groups influence the likelihood of a conviction.
  - Punishment Severity: Quantifies the severity of punishments, including prison sentence lengths, fines, or other penalties. We'll standardize these penalties by converting sentences into years or fines into monetary values adjusted for inflation.


**2. Data Preprocessing**


For data preprocessing, I extract the names of judges, prosecutors, and defense attorneys from the text data using regular expressions (regex). This involves parsing court decision texts to accurately identify the legal professionals involved in each case, paying particular attention to the grammatical structure and variations in legal terminology in Russian. Regex is a powerful tool for pattern matching in text. By defining specific patterns, I can search for and extract relevant information from court decision texts. This approach ensures accurate extraction of names of judges, prosecutors, and defense attorneys even when they appear in different grammatical forms.

### Regex Patterns:

- **Judges**: Patterns like `судья\s+([\w\s]+(?:в|а|е|ой|ью)?)` matched the title "судья" followed by a name with possible case endings (e.g., Иванов А.А.).
- **Prosecutors**: Patterns like `прокурор\s+([\w\s]+(?:а|у|ом|е)?)` matched the title "прокурор" followed by a name with case endings.
- **Defense Attorneys**: Patterns like `адвокат\s+([\w\s]+(?:а|у|ом|е)?)` matched the title "адвокат" followed by a name with case endings.

Similarly, extracting punishment severity involves identifying and quantifying details related to the sentences imposed, such as the length of prison terms, types of penal colonies, fines, and other penalties. These details are then converted into a standardized severity metric, such as total years of punishment.

### Regex Patterns for Punishment Severity:

- **Years of Imprisonment**: The pattern `(\d+)\s*лет` matches sentences expressed in years. Directly added to the severity score as the number of years.
- **Months of Imprisonment**: The pattern `(\d+)\s*месяцев` matches sentences expressed in months and converts them to years. Converted to a fraction of a year and then added to the severity score.
- **Types of Penal Colonies**: The pattern `(общего режима|строгого режима|особого режима)` matches different types of penal colonies and assigns corresponding severity values:
  - General Regime penal colonies are considered less severe compared to strict or special regime colonies. The value of 2 is chosen to reflect this lesser severity while still recognizing that it involves imprisonment.
  - Strict Regime penal colonies are more severe than general regime colonies, involving stricter conditions and more restrictive environments. The value of 5 is chosen to represent this increased severity.
  - Special Regime penal colonies are the most severe, reserved for the most dangerous offenders or those with severe sentences. The value of 10 is chosen to reflect the highest level of severity.
- **Fines**: The pattern `штраф\s*в\s*размере\s*(\d+)` matches monetary fines and normalizes them by a factor. Fines are normalized by a factor to reflect their severity relative to other punishment types. For instance, a fine is divided by 10,000 to scale it appropriately.
- **Probation**: The pattern `условно\s*на\s*(\d+)\s*лет` matches probation sentences and subtracts them from the severity score.
- **Pre-trial Detention**: The pattern `временное\s*содержание\s*под\s*стражей\s*(\d+)\s*дней` matches pre-trial detention periods and converts them to years.

### Types of Punishments and Their Conversion

| Punishment Type         | Detail                                           | Severity Rating                     |
|-------------------------|--------------------------------------------------|-------------------------------------|
| **Imprisonment**        |                                                  |                                     |
| - Years of imprisonment | Directly extracted from text                     | + Number of years                   |
| - Months of imprisonment| Converted to years                               | + Number of months / 12             |
| **Types of Penal Colonies** |                                             |                                     |
| - General Regime        | Общего режима                                    | + 2                                 |
| - Strict Regime         | Строгого режима                                  | + 5                                 |
| - Special Regime        | Особого режима                                   | + 10                                |
| **Fines**               |                                                  |                                     |
| - Monetary fines        | Normalized by factor (e.g., per 10,000 rubles)   | + Fine amount / 10,000              |
| **Additional Restrictions**|                                              |                                     |
| - Probation             | Условно (years)                                  | Minus number of years               |
| - Pre-trial detention   | Временное содержание под стражей (days)          | + Number of days / 365              |
| - Additional restrictions| Other types of legal restrictions               | + 1 (for each restriction identified) |
