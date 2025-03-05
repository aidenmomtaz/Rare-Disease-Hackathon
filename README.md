# PhenoRare

## Introduction
When hearing from diverse perspectives about the unique challenges of rare diseases, a resounding problem our team identified was the difficulty of achieving a timely diagnosis. Whether the root cause was clinician unfamiliarity with the disease and its presentation (due to its hyper-rare nature), difficulty of the patient or their caregiver in advocating for further tests, or simply a disease that is so unique only a few hundred people across the globe are diagnosed with it. Our solution, PhenoRare, solves each of these painpoints by providing a platform for patients and doctors to objectively determine the best screen or disease candidates for a patient (without requiring the doctor to keep track of thousands of rare diseases) and create a network of undiagnosed/uncured patients, allowing future scientific advances to impact all known patients with the disease. Our app does this by using an enhanced version of Phrank combined with an OpenAI integration and a simple UI, allowing patients to input their symptoms without needing extensive medical or Human Phenotype Ontology knowledge, thereby making agency over one’s records and screens more accessible. 

## Our Method
### Phrank:
Phrank is a Python package that can compute the similarity score between two phenotype sets based on a hierarchical phenotype ontology tree and a map of diseases to their associated phenotypes. By default, Phrank uses a relatively extensive disease to phenotype map with 4,000+ diseases. There are two major issues with this default map: it doesn’t include many rare diseases or the frequency of observing phenotypes associated with a disease. PhenoRare addresses both of these issues by modifying the Phrank algorithm to utilize a database of rare diseases and the frequencies of phenotypes associated with those diseases from Orphanet – a website whose purpose is to gather information about rare diseases to ultimately improve diagnosis, care, and treatment. This adjusted Phrank algorithm should improve accuracy and reduce the chance of false positives when predicting rare diseases. PhenoRare also utilizes the Phrank algorithm to compute the similarity between patients in our Undiagnosed Network (more information in Workflow section) based on their phenotype sets so physicians can be notified if a similar patient is diagnosed with a newly discovered disease. 

### Symptom Input:
Rather than require patients to input their symptoms using complicated and esoteric HPO terms or relying on doctors to transcribe this information, PhenoRare puts agency back in the hands of the patient or their caregiver by allowing easy input of symptoms in common language. Our code includes an API integration with OpenAI’s 4.0 model, sending user inputs as queries to the model and receiving back HPO terms. These terms are then fed to the Phrank algorithm to produce disease matches. It was important to our team that PhenoRare be completely accessible and easy-to-use for anyone with a mobile phone, regardless of their scientific or medical knowledge. 

### Workflow:
A simple product workflow outlines the steps a patient takes to go from symptom to prediction within minutes:
User is prompted to enter their symptom in natural language. Under the hood, an LLM integration efficiently converts and reports their symptom as an HPO term. User enters as many symptoms as they’d like before submitting.
PhenoRare uses our proprietary enhanced Phrank model to calculate and output the top 5 disease matches based on a user’s symptom input. 
User is asked if they have already been screened for or ruled out the predicted diseases 
If a user has already been screened for all predicted diseases, they are added to our PhenoRare Undiagnosed Diseases Network – following future development, inclusion in this network would allow doctors, researchers, or drug development companies a consolidated method of distributing their new research or therapeutics to all patients with a similar disease presentation

## Discussion & Next Steps
The key outcomes of our workflow are enhanced objectivity in diagnosing and screening for patients with potentially highly rare diseases, as well as an increased agency over the diseases their doctor is considering. This should reduce patient frustration with redundant misdiagnoses and speed up the overall process of diagnosis. Additionally, our future development of the PhenoRare Undiagnosed Diseases Network creates an exponential benefit for both the patients who use PhenoRare as well as scientists wishing to develop new therapeutics for rare diseases by creating a streamlined process for new information to be accessed and shared. Using our existing Phrank framework, we were able to compare patients with a highly unique phenotype set to existing patients in the database, allowing multiple patients with the same undiagnosed set of symptoms to be grouped together. This way, if a researcher was able to find a diagnosis for one of these patients, all of their doctors could be notified and empowered to act promptly to screen for and treat this disease. 

To improve PhenoRare further, we could implement a system where patients can also input the severity of their symptoms, which would be incorporated into the modified Phrank algorithm to predict possible diseases. However, a potential drawback of adding this feature is that it may introduce some bias as different people may report symptom severity differently. Moreover, we can conduct more thorough and extensive testing on the threshold value for determining whether the phenotype sets of two patients are a match and correspond to the same undiagnosed disease. Finally, we will continuously add diseases to the disease-to-phenotype database to increase the scope of PhenoRare as much as possible. 


