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

The concept of stable working groups in courtrooms involves the same judge, prosecutor, and defense attorney collaborating on multiple cases. Extensively explored in Western legal studies, this idea is well-documented in the US legal system by researchers like Eisenstein and Jacob (1977) and Nardulli (1978). These courtroom elites develop common understandings, cooperative techniques, and shared norms, influencing court decisions.

In Russia, this concept translates similarly, though with unique aspects due to different legal traditions and procedures. Stable working groups in the Russian legal system are identified by observing recurring combinations of judges, prosecutors, and defense attorneys handling many cases together over time. These repeated interactions and established professional connections can lead to more predictable and potentially more severe judicial decisions.

When legal professionals frequently work together, it can influence judicial outcomes and the severity of punishments. Regular interactions among the same judge, prosecutor, and defense attorney can result in more predictable court outcomes, as familiarity with each other's expectations and styles leads to consistent decisions. This familiarity can streamline the trial process, enhancing predictability and case management (Eisenstein & Jacob, 1977; Nardulli, 1978).

However, repeated interactions can also introduce bias. Over time, a close working relationship between a judge and a prosecutor might lead to favoritism or harsher sentencing. A judge might align more closely with the prosecutor's perspective due to their ongoing collaboration, resulting in more severe punishments for defendants (Haynes et al., 2010). Stable working groups often handle cases more efficiently, leading to quicker resolutions but not necessarily more lenient sentences. Instead, the court might process more cases, maintaining a consistent rate of convictions and penalties. Research by Johnson (2006) indicates that judges who frequently work with the same attorneys can expedite proceedings, leading to uniform and sometimes stricter sentencing practices.


