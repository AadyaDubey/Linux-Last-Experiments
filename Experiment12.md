# Experiment 12: Building a Rule-Based Expert System using Shell Scripting

**Name:** Aadya Dubey  
**Roll No.:** 590029213

* * *

# Theory
*  Process Automation and Job Scheduling: Automating repetitive tasks using shell scripts
*  System Administration Scripts
*  Managing services and daemons

***

# Aim
The objective of this lab exercise is to build a simple rule-based expert
system using shell scripting. The expert system will provide recommendations
based on a set of predefined rules.

***
***

## Script:
```bash
#!/bin/bash

display_header() {
    echo "-------------------------------------------"
    echo "      SIMPLE MEDICAL EXPERT SYSTEM"
    echo "-------------------------------------------"
 
}

get_symptoms() {
    echo "Enter your symptoms:"
    read -r user_input
    symptoms=$(echo "$user_input" | tr 'A-Z' 'a-z')
}

evaluate_rules() {
    local matched=false
    echo
    echo " RECOMMENDATIONS "

    if [[ "$symptoms" == *"fever"* ]]; then
        echo "- Fever detected."
        echo "  Recommendation:"
        echo "   • Rest and drink plenty of fluids."
        echo "   • Medication (example): Paracetamol (e.g., 500 mg) as per label/doctor’s advice."
        matched=true
        echo
    fi

    if [[ "$symptoms" == *"sore throat"* ]] || [[ "$symptoms" == *"throat pain"* ]]; then
        echo "- Sore throat detected."
        echo "  Recommendation:"
        echo "   • Gargle with warm saltwater 2–3 times a day."
        echo "   • Medication (example): Lozenges (e.g., Strepsils) as directed on the pack."
        matched=true
        echo
    fi

    if [[ "$symptoms" == *"cough"* ]] && ([[ "$symptoms" == *"congestion"* ]] || [[ "$symptoms" == *"cold"* ]]); then
        echo "- Cough with congestion detected."
        echo "  Recommendation:"
        echo "   • Drink warm fluids and inhale steam (with care)."
        echo "   • Medication (example): Cough syrup with expectorant (e.g., ambroxol-based) as per label/doctor."
        matched=true
        echo
    fi

    if [[ "$symptoms" == *"cough"* ]] && [[ "$symptoms" != *"congestion"* ]] && [[ "$symptoms" != *"cold"* ]]; then
        echo "- Cough detected."
        echo "  Recommendation:"
        echo "   • Sip warm water frequently, avoid dust/smoke."
        echo "   • Medication (example): Cough syrup with dextromethorphan (dry cough) as indicated on label/doctor."
        matched=true
        echo
    fi

    if [[ "$symptoms" == *"headache"* ]]; then
        echo "- Headache detected."
        echo "  Recommendation:"
        echo "   • Rest in a quiet, dark room; reduce screen time."
        echo "   • Medication (example): Paracetamol or ibuprofen as per package instructions/doctor."
        matched=true
        echo
    fi

    if [[ "$symptoms" == *"cold"* ]] || [[ "$symptoms" == *"runny nose"* ]] || [[ "$symptoms" == *"sneezing"* ]]; then
        echo "- Common cold–like symptoms detected."
        echo "  Recommendation:"
        echo "   • Stay warm; drink warm water/tea."
        echo "   • Medication (example): Antihistamine (e.g., cetirizine) and saline nasal spray as per instructions doctor."
        matched=true
        echo
    fi

    if [[ "$symptoms" == *"vomiting"* ]]; then
        echo "- Vomiting detected."
        echo "  Recommendation:"
        echo "   • Take small sips of ORS or clear fluids frequently."
        echo "   • Avoid solid food until vomiting reduces."
        echo "   • Medication (example): Antiemetic (e.g., ondansetron) strictly as prescribed by a doctor."
        matched=true
        echo
    fi

    if [[ "$matched" == false ]]; then
        echo "- Your symptoms did not match any specific rule."
        echo "  General Recommendation:"
        echo "   • Take adequate rest."
        echo "   • Drink plenty of water."
        echo "   • Eat light, healthy food."
        echo "   • Consult a doctor or pharmacist before taking any medicine."
        echo
    fi

}

display_header
get_symptoms
evaluate_rules
exit 0


```
## Output:
 
## Logic & Rules Implemented and Modifications 
### Logics 

* The script displays a header to indicate the start of the expert system.
  
	``` 
	  display_header() {
	    echo "-------------------------------------------"
	    echo "      SIMPLE MEDICAL EXPERT SYSTEM"
	    echo "-------------------------------------------"
	}
	```


* The user is prompted to enter symptoms using the read command.
 
  ```
  echo "Enter your symptoms (separated by space):"
  read -r user_input
  ```

* The input is converted to lowercase using the `tr` command for case-insensitive matching.
	```
 	symptoms=$(echo "$user_input" | tr 'A-Z' 'a-z')
	```

* The program checks the input using multiple if conditional statements.
  ```
  if [[ "$symptoms" == *"fever"* ]]; then
  if [[ "$symptoms" == *"sore throat"* ]]; then
  ```

* When a rule matches, the corresponding recommendation and medication are displayed.
  ```
   echo "- Fever detected."
   echo "  Recommendation:"
   echo "   • Rest and drink plenty of fluids."
   echo "   • Medication (example): Paracetamol (e.g., 500 mg)"
  ```

* A Boolean variable matched is used to track whether any rule has matched.
  ```
  local matched=false
  matched=true
  ```


* If no rule matches, a general health recommendation is displayed.
  ```
  if [[ "$matched" == false ]]; then
    echo "- Your symptoms did not match any specific rule."
    echo "  General Recommendation:"
  fi
  ```

* After displaying results, the program terminates using `exit 0`.

  ```
   exit 0
  ```

### Modified Rules 
    
I created a total of 7 rules in the expert system, each of which contains 2–3 conditional checks to accurately detect and recommend solutions for different symptoms.

* Fever Rule
   ```
   if [[ "$symptoms" == *"fever"* ]]; then
   ```
* Soar Throat Rule
   ```
   if [[ "$symptoms" == *"sore throat"* ]] || [[ "$symptoms" == *"throat pain"* ]]; then
   ```
* Cough and Congestion Rule
   ```
    if [[ "$symptoms" == *"cough"* ]] && ([[ "$symptoms" == *"congestion"* ]] || [[ "$symptoms" == *"cold"* ]]); then
   ```
* Only Cough Rule 
   ```
    if [[ "$symptoms" == *"cough"* ]] && [[ "$symptoms" != *"congestion"* ]] && [[ "$symptoms" != *"cold"* ]]; then
   ```
* Headache Rule
   ```
   if [[ "$symptoms" == *"headache"* ]]; then
   ```  
* Cold/Runny Nose Rule
  ```
   if [[ "$symptoms" == *"cold"* ]] || [[ "$symptoms" == *"runny nose"* ]] || [[ "$symptoms" == *"sneezing"* ]]; then
  ```
* Vomiting Rule
  ```
  if [[ "$symptoms" == *"vomiting"* ]]; then
  ```
 
 ***

 