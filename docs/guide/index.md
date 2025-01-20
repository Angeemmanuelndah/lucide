import React, { useState } from 'react';
import { Card, CardHeader, CardTitle, CardContent } from '@/components/ui/card';
import { Alert, AlertDescription } from '@/components/ui/alert';
import { ArrowRight, Check, X } from 'lucide-react';

const QuizGame = () => {
  const [currentQuestion, setCurrentQuestion] = useState(0);
  const [keyword, setKeyword] = useState('');
  const [explanation, setExplanation] = useState('');
  const [showAnswer, setShowAnswer] = useState(false);
  const [score, setScore] = useState(0);
  const [userAnswer, setUserAnswer] = useState('');
  const [answered, setAnswered] = useState(false);
  const [studentAnswers, setStudentAnswers] = useState([]);
  const [showResults, setShowResults] = useState(false);

  const saveAnswer = () => {
    const answer = {
      questionId: questions[currentQuestion].id,
      question: questions[currentQuestion].question,
      keywords: keyword,
      studentExplanation: explanation,
      selectedAnswer: userAnswer,
      correctAnswer: questions[currentQuestion].correctAnswer,
      isCorrect: userAnswer === questions[currentQuestion].correctAnswer
    };

    setStudentAnswers(prev => [...prev.filter(a => a.questionId !== answer.questionId), answer]);
  };

  const questions = [
    {
      id: 1,
      question: "A 7-year-old girl has been twice treated with antibacterial agents for urinary tract infection. US shows no severe renal defects. The child presents with recurrence of leukocyturia and bacteriuria, elevated body temperature up to 38.5oC, and pain in her left lumbar area. What examination should be conducted first to clarify the cause of urinary infection recurrence?",
      options: {
        A: "Immunogram",
        B: "Retrograde pyelography",
        C: "Radioisotope renography",
        D: "Excretory urography",
        E: "Micturating cystourethrography"
      },
      correctAnswer: "E",
      explanation: "Micturating cystourethrography is essential for diagnosing vesicoureteral reflux, a common cause of recurrent UTIs in children."
    },
    {
      id: 2,
      question: "A 59-year-old man complains of pain in his left eye and left side of his head, significant vision impairment of the left eye, nausea, and vomiting. Visual acuity of the right eye is 1.0. Visual acuity of the left eye is 0.03, attempts at correction bring no improvement. Right eye intraocular pressure - 21 mm Hg, left eye intraocular pressure 65 mm Hg. What is the most likely diagnosis?",
      options: {
        A: "Panophthalmitis of the left eye",
        B: "Endophthalmitis of the left eye",
        C: "Stage II intraocular tumor of the left eye",
        D: "Acute iridocyclitis of the left eye",
        E: "Acute attack of glaucoma of the left eye"
      },
      correctAnswer: "E",
      explanation: "The combination of very high intraocular pressure (65 mmHg), dilated unresponsive pupil, shallow anterior chamber, and corneal edema are classic signs of acute angle-closure glaucoma."
    },
    {
      id: 3,
      question: "A 63-year-old woman suddenly developed an asphyxia attack at night. She has a 15-year history of hypertension and had a myocardial infarction 2 years ago. Position is orthopneic, skin pale with cold sweat. BP - 210/130 mm Hg, RR - 38/min. Throughout lungs, crackling sounds becoming bubbling in lower segments. What is the most likely complication?",
      options: {
        A: "Bronchial asthma attack",
        B: "Acute right ventricular failure",
        C: "Pulmonary embolism",
        D: "Acute left ventricular failure",
        E: "Paroxysmal tachycardia"
      },
      correctAnswer: "D",
      explanation: "The orthopneic position, pulmonary crackles, and history of hypertension and MI suggest acute left ventricular failure causing pulmonary edema."
    },
    {
      id: 4,
      question: "A 3-week-old infant developed large, flaccid vesicles with purulent contents on the skin of chest and abdomen. The vesicles rupture quickly. Make the provisional diagnosis:",
      options: {
        A: "Toxic erythema",
        B: "Pemphigus neonatorum",
        C: "Vesiculopustulosis",
        D: "Pseudofurunculosis",
        E: "Pemphigus syphiliticus"
      },
      correctAnswer: "B",
      explanation: "The presence of large, flaccid vesicles with purulent contents that rupture quickly in a newborn is characteristic of pemphigus neonatorum."
    },
    {
      id: 5,
      question: "During an outdoors school event in hot weather, a 10-year-old girl lost her consciousness. Body temperature - 36.7oC. Objectively her skin is pale and cold to touch, her pupils are dilated. Blood pressure - 90/50 mm Hg. Heart rate - 58/min. What pathology occurred in this case?",
      options: {
        A: "Sunstroke",
        B: "Sympathicotonic collapse",
        C: "Paralytic collapse",
        D: "Syncope",
        E: "-"
      },
      correctAnswer: "D",
      explanation: "The sudden loss of consciousness with pale, cold skin, low blood pressure, and bradycardia in a hot environment suggests vasovagal syncope."
    },
    {
      id: 6,
      question: "A 32-year-old woman complains of tumorlike formation on the anterior surface of her neck that appeared 2 years ago. Within the last 3 months the tumor has been rapidly growing. It hinders swallowing and impairs speech. In the right lobe of the thyroid gland there is a dense lumpy node 3.0x3.5 cm that moves during swallowing. Scanning image shows a 'cold nodule' in the thyroid gland. Make the provisional diagnosis:",
      options: {
        A: "Thyroid adenoma",
        B: "Thyroid cancer",
        C: "Autoimmune thyroiditis",
        D: "Thyroid cyst",
        E: "Nodular goiter"
      },
      correctAnswer: "B",
      explanation: "Rapid growth, compression symptoms, and a cold nodule on scan are suspicious for thyroid cancer."
    },
    {
      id: 7,
      question: "A 43-year-old man complains of a protrusion in the right inguinal region that enlarges due to strain. Objectively in the right inguinal region an elastic protrusion 8x5 cm is visible. On palpation it disappears, leaving an empty space 4x4 cm between the pedicles of the Poupart ligament. 'Cough push' sign is positive. Make the diagnosis:",
      options: {
        A: "Cyst of the right spermatic cord",
        B: "Right-sided reducible femoral hernia",
        C: "Right-sided inguinal lymphadenitis",
        D: "Right-sided reducible inguinal hernia",
        E: "Right-sided reducible arcuate line hernia"
      },
      correctAnswer: "D",
      explanation: "The location, reducibility, and positive cough impulse are characteristic of an inguinal hernia."
    },
    {
      id: 8,
      question: "A 36-year-old man complains of marked dyspnea and cardiac pain. He describes his disease to the case of influenza that he had 2 weeks ago. The face is swollen, cyanotic, cervical veins are distended. Heart borders are extended, sounds muffled, heart rate = Ps = 118/min., BP is 90/60 mm Hg. ECG shows low voltage. X-ray shows trapezoidal cardiac silhouette. What is the best treatment?",
      options: {
        A: "Glucocorticosteroids",
        B: "Antibiotics",
        C: "Pericardectomy",
        D: "Diuretics",
        E: "Pericardial puncture"
      },
      correctAnswer: "E",
      explanation: "The symptoms suggest cardiac tamponade following post-viral pericarditis, requiring immediate pericardiocentesis."
    },
    {
      id: 9,
      question: "A 57-year-old woman complains of weakness, dyspnea, loss of appetite, and liquid feces. Blood test shows macrocytic anemia (Hb 56 g/L, color index 1.4) with leukopenia and thrombocytopenia. What changes can be expected in the bone marrow puncture material?",
      options: {
        A: "Presence of blast cells",
        B: "Prevalence of lymphoid tissue",
        C: "Increased number of sideroblasts",
        D: "Prevalence of megaloblasts",
        E: "Erythroid hyperplasia"
      },
      correctAnswer: "D",
      explanation: "The macrocytic anemia with pancytopenia suggests megaloblastic anemia, likely due to B12 deficiency, which would show megaloblasts in bone marrow."
    },
    {
      id: 10,
      question: "A 28-year-old man complains of skin rash and itching on both hands for 1.5 years. The exacerbation relates to occupational contact with formaldehyde resins. Against the background of erythema there are papulae, vesicles, erosions, crusts, and scales. What is the most likely pathology?",
      options: {
        A: "Simple contact dermatitis",
        B: "Allergic dermatitis",
        C: "Idiopathic eczema",
        D: "Erythema multiforme",
        E: "Occupational eczema"
      },
      correctAnswer: "E",
      explanation: "The chronic nature, occupational exposure, and characteristic lesions indicate occupational eczema."
    },
    {
      id: 11,
      question: "A 30-year-old woman during regular gynecological examination was detected to have dark blue 'punctulated perforations' on the vaginal portion of the uterine cervix. What investigation method would be most informative for diagnosis confirmation?",
      options: {
        A: "Colposcopy, target biopsy of the cervix",
        B: "Curettage of the uterine cavity",
        C: "Hormone testing",
        D: "US of the lesser pelvis",
        E: "Hysteroscopy"
      },
      correctAnswer: "A",
      explanation: "Colposcopy with targeted biopsy is the gold standard for diagnosing cervical endometriosis and other cervical lesions."
    },
    {
      id: 12,
      question: "A 13-year-old girl has 30% excessive body mass, started gaining weight at age 3. Family history of obesity. Height and sexual development normal. Appetite excessive. BP 120/80 mm Hg. Even fat distribution, no stretch marks. Juvenile acne present. What type of obesity is it?",
      options: {
        A: "Alimentary constitutive obesity",
        B: "Hypothalamic obesity",
        C: "Adrenal obesity",
        D: "Hypothalamic syndrome of puberty",
        E: "Hypothyroid obesity"
      },
      correctAnswer: "A",
      explanation: "The gradual onset from early childhood, family history, and absence of endocrine symptoms indicate alimentary constitutional obesity."
    }
,
    {
      id: 13,
      question: "A 7-year-old boy has severe pulmonary mucoviscidosis (cystic fibrosis). He has dyspnea and blood expectoration. He presents with lagging physical development, acrocyanosis, hepatomegaly, drumstick fingers. Provisional diagnosis of chronic pulmonary heart disease is made. What examination would be most informative for confirmation?",
      options: {
        A: "Doppler echocardiography",
        B: "Electrocardiography",
        C: "Chest X-ray",
        D: "Rheography of the pulmonary artery",
        E: "Ultrasound of the liver"
      },
      correctAnswer: "A",
      explanation: "Doppler echocardiography is the most informative test for evaluating pulmonary hypertension and right heart function in cor pulmonale."
    },
    {
      id: 14,
      question: "A 51-year-old man complains of vomiting blood. Heavy alcohol use history. First developed jaundice at 40. Presents with jaundice, stellate vascular pattern, malnutrition, ascites. Edge of liver tapered and painless, +3 cm, spleen +2 cm. Blood: Hb- 80 g/L, leukocytes - 3·109/L, platelets - 85·109/L. What is the cause of portal hypertension?",
      options: {
        A: "Constrictive pericarditis",
        B: "Hemochromatosis",
        C: "Thrombosis of the splenic vein",
        D: "Budd-Chiari syndrome",
        E: "Hepatic cirrhosis"
      },
      correctAnswer: "E",
      explanation: "The history of alcoholism, physical findings of cirrhosis, and pancytopenia indicate alcoholic cirrhosis as the cause of portal hypertension."
    },
    {
      id: 15,
      question: "A 30-year-old multigravida has been in labour for 18 hours. Pushing stage began 2 hours ago. Fetal heart rate clear, rhythmic, 136/min. Complete cervical dilatation, fetal head in pelvic outlet plane. Diagnosed with primary uterine inertia. What is the further tactics?",
      options: {
        A: "Vacuum extraction of the fetus",
        B: "Outlet forceps",
        C: "Labour stimulation",
        D: "Cesarean section",
        E: "Skin-head Ivanov's forceps"
      },
      correctAnswer: "A",
      explanation: "With prolonged second stage and uterine inertia but reassuring fetal status, vacuum extraction is appropriate as it's less traumatic than forceps."
    },
    {
      id: 16,
      question: "At a railroad crossing a passenger train collided with a bus. 26 bus passengers died, another 18 received mechanical injuries of varying severity. Where will professional medical aid be provided and by whom?",
      options: {
        A: "At the site of the accident; specialized second-response emergency teams",
        B: "In medico-prophylactic institutions; general physicians and surgeons",
        C: "In medico-prophylactic institutions; specialized second-response emergency teams",
        D: "At the site of the accident; first-response emergency teams",
        E: "In medical institutions; all listed types of healthcare workers"
      },
      correctAnswer: "C",
      explanation: "In mass casualty incidents, definitive care is provided in medical institutions by specialized teams after initial triage and stabilization."
    }
,
    {
      id: 17,
      question: "A 38-year-old patient brought to surgical department complains of general weakness, black stool. Patient is pale, has dotted hemorrhages on torso and extremities. Digital investigation shows black feces. Blood test: Hb- 108 g/L, thrombocytopenia. Similar condition occurred 1 year ago. Make the diagnosis:",
      options: {
        A: "Thrombocytopenic purpura",
        B: "Nonspecific ulcerative colitis",
        C: "Hemophilia",
        D: "Ulcerative bleeding",
        E: "Rectal tumor"
      },
      correctAnswer: "A",
      explanation: "The combination of thrombocytopenia, petechial hemorrhages, and recurrent episodes suggests thrombocytopenic purpura."
    },
    {
      id: 18,
      question: "Mother noticed on her 5-year-old child's head a round 'bald' spot 3 cm in diameter. All hairs in the focus are broken off at 5-6 mm length. The day before the child was petting a stray cat. Make the diagnosis:",
      options: {
        A: "Microsporia",
        B: "Superficial trichophytosis",
        C: "Deep trichophytosis",
        D: "Alopecia areata",
        E: "Psoriasis"
      },
      correctAnswer: "A",
      explanation: "The round patch of broken hairs following contact with a cat is characteristic of microsporia, a fungal infection commonly transmitted by cats."
    },
    {
      id: 19,
      question: "A 3-year-old child has pain in legs, fever, loss of appetite. Pale skin and mucosa, hemorrhagic rash. Enlarged painless dense lymph nodes. Bones, joints, abdomen painful. Liver and spleen enlarged. Blood: Hb- 88 g/L, platelets - 80·109/L, leukocytes - 25.8·109/L, lymphoblasts - 70%, ESR- 52 mm/hour. Diagnosis?",
      options: {
        A: "Thrombocytopenic purpura",
        B: "Hemorrhagic vasculitis",
        C: "Acute leukemia",
        D: "Acute rheumatic fever",
        E: "Infectious mononucleosis"
      },
      correctAnswer: "C",
      explanation: "High WBC count with 70% lymphoblasts, anemia, thrombocytopenia, and organomegaly are diagnostic for acute lymphoblastic leukemia."
    },
    {
      id: 20,
      question: "In the inpatient gynecological unit within a year 6500 women underwent treatment. They spent there a total of 102000 bed-days. What indicator of the gynecological unit work can be calculated based on these data?",
      options: {
        A: "Number of beds by hospital department",
        B: "Average length of inpatient stay",
        C: "Average bed occupancy rate per year",
        D: "Planned bed occupancy rate per year",
        E: "Bed turnover rate"
      },
      correctAnswer: "B",
      explanation: "Average length of stay can be calculated by dividing total bed-days (102000) by number of patients (6500) = 15.7 days."
    },
    {
      id: 21,
      question: "A 63-year-old man complains of weakness and pressure in left subcostal area for a year. Participated in Chernobyl cleanup. Skin pale, liver +3 cm, spleen +10 cm. Blood: leukocytes - 46·109/L, blasts - 2%, promyelocytes - 10%, myelocytes 18%, band neutrophils - 27%, segmented - 10%, lymphocytes - 12%, eosinophils - 6%, basophils - 3%, monocytes - 2%. Likely diagnosis?",
      options: {
        A: "Chronic myeloleukemia",
        B: "Hepatic cirrhosis",
        C: "Acute leukemia",
        D: "Hemolytic anemia",
        E: "Chronic lymphatic leukemia"
      },
      correctAnswer: "A",
      explanation: "High WBC with full spectrum of myeloid precursors and prominent splenomegaly is characteristic of chronic myeloid leukemia."
    },
    {
      id: 22,
      question: "An 18-year-old patient always obeys others and adapts needs to demands of people he depends on. Excessively defers to wishes and makes others responsible for his wellbeing. Cannot defend interests and needs support. Profile formed in childhood, remains unchanged, hinders adaptation. What psychic disorder is observed?",
      options: {
        A: "Dependent personality disorder",
        B: "Anxiety personality disorder",
        C: "Anankastic personality disorder",
        D: "Psychopathy-like state",
        E: "Markedly accentuated personality"
      },
      correctAnswer: "A",
      explanation: "The pattern of submissive and clinging behavior, excessive need for care, and difficulty making everyday decisions are characteristic of dependent personality disorder."
    },
    {
      id: 23,
      question: "A 38-year-old woman has weakness, sleepiness, joint pain, weight gain despite low appetite, and constipation. Dry thickened skin, puffy amimic face, narrowed palpebral fissures, thick tongue, hoarse voice. Heart sounds weak, pulse 56/min. Low free T4. Regular treatment needed:",
      options: {
        A: "Thyroxine",
        B: "Mercazolil",
        C: "Lithium carbonate",
        D: "Furosemide",
        E: "Calcium gluconate"
      },
      correctAnswer: "A",
      explanation: "The clinical features and low T4 indicate hypothyroidism requiring thyroid hormone replacement with thyroxine."
    },
    {
      id: 24,
      question: "A 10-year-old boy with arthritis and myocarditis was diagnosed with juvenile rheumatoid arthritis. What symptom is most contributive for diagnosis?",
      options: {
        A: "Reduced mobility of joints in morning",
        B: "Affection of large joints",
        C: "Regional hyperemia of joints",
        D: "Enlarged heart",
        E: "Increased heart rate"
      },
      correctAnswer: "A",
      explanation: "Morning stiffness is a hallmark diagnostic feature of juvenile rheumatoid arthritis, distinguishing it from other forms of arthritis."
    }
,
    {
      id: 25,
      question: "A 50-year-old patient was brought with complaints of blood in urine. Urination is painless and undisturbed. Macrohematuria for 3 days. Kidneys cannot be palpated, suprapubic area normal, genitalia nonpathologic. Prostate not enlarged, painless, normal structure. Cystoscopy normal. Most likely diagnosis?",
      options: {
        A: "Necrotic papillitis",
        B: "Dystopic kidney",
        C: "Varicocele",
        D: "Bladder tuberculosis",
        E: "Renal carcinoma"
      },
      correctAnswer: "E",
      explanation: "Painless gross hematuria in an older adult with normal cystoscopy suggests upper urinary tract pathology, most concerning for renal cell carcinoma."
    },
    {
      id: 26,
      question: "A 33-year-old man has multiple rashes on torso and limb extensor surfaces. Rashes itch and form plaques covered with silver-white scales that easily flake off. Grattage test shows: stearin spot, terminal film, and punctate hemorrhage. Suspected diagnosis?",
      options: {
        A: "Secondary papular syphilid",
        B: "Lichen ruber planus",
        C: "Pyoderma",
        D: "Parapsoriasis",
        E: "Psoriasis"
      },
      correctAnswer: "E",
      explanation: "The characteristic silvery scales, positive grattage phenomena (Auspitz sign), and distribution pattern are diagnostic for psoriasis."
    },
    {
      id: 27,
      question: "A 34-year-old man has pale edema of face, feet, shins, and lumbar area, BP 160/100 mmHg, and weakness. History of ulcerative colitis. Kidneys not palpable. Blood: ESR 50mm/hr. Urine: proteins 3.5g/L, RBC 7-10, WBC 5-6. Daily proteinuria 6g. What additional test needed?",
      options: {
        A: "Survey and excretory urography",
        B: "Renal ultrasound",
        C: "Urinalysis for Bence-Jones protein",
        D: "Radioisotopic examination of kidneys",
        E: "Gingival biopsy for amyloid disease"
      },
      correctAnswer: "E",
      explanation: "With history of chronic inflammatory disease and nephrotic syndrome, secondary amyloidosis should be suspected; gingival biopsy can confirm the diagnosis."
    },
    {
      id: 28,
      question: "A woman polisher using grinding machine for 1.5 years complains of white finger discoloration when nervous. No visible changes. Grip strength 25kg, algesimetry 0.1;0.3;0.5. Cold stimulus extremely positive on limbs. Internal organs normal. Diagnosis?",
      options: {
        A: "Polyneuritis",
        B: "Syringomyelia",
        C: "Vibration disease",
        D: "Raynaud syndrome",
        E: "Raynaud disease"
      },
      correctAnswer: "C",
      explanation: "Occupational exposure to vibration with characteristic vasospastic symptoms (white finger) indicates vibration disease/hand-arm vibration syndrome."
    },
    {
      id: 29,
      question: "A 23-year-old man has facial edemas, headache, dizziness, low urinary output, and dark red urine after acute tonsillitis. Face edematous, skin pale, temp 37.4°C, BP 170/110 mmHg. Heart sounds muffled, II sound accentuated over aorta. Most likely etiological factor?",
      options: {
        A: "Streptococcus pyogenes",
        B: "Staphylococcus aureus",
        C: "Staphylococcus saprophyticus",
        D: "Beta-hemolytic streptococcus",
        E: "Streptococcus viridans"
      },
      correctAnswer: "D",
      explanation: "Post-streptococcal glomerulonephritis following throat infection is typically caused by beta-hemolytic streptococcus."
    },
    {
      id: 30,
      question: "During examination a naval cadet was found to have a painless dense ulcer 1.5x0.5 in size in perianal area at 2 o'clock position. Ulcer floor resembles 'old fat'. Provisional diagnosis?",
      options: {
        A: "Rectal fissure",
        B: "Hard syphilitic chancre of the rectum",
        C: "Anal crypt suppuration",
        D: "Anal cancer",
        E: "Rectal fistula"
      },
      correctAnswer: "B",
      explanation: "The painless ulcer with characteristic 'old fat' appearance of the base is typical of a primary syphilitic chancre."
    },
    {
      id: 31,
      question: "A 35-year-old man has fatigue, palpitations, 'visual snow', dizziness. History of peptic ulcer. Skin pale, systolic murmur at apex, HR 100/min, BP 100/70 mmHg. Epigastrium tender. Blood: RBC 3.2·1012/L, Hb 100 g/L, color index 0.95. Most likely anemia type?",
      options: {
        A: "Hemolytic anemia",
        B: "Chronic iron-deficiency anemia",
        C: "Hypoplastic anemia",
        D: "Sideroblastic anemia",
        E: "Posthemorrhagic anemia"
      },
      correctAnswer: "B",
      explanation: "History of peptic ulcer with microcytic anemia (color index <1) suggests chronic iron deficiency from gastrointestinal blood loss."
    },
    {
      id: 32,
      question: "A 35-year-old insulin dependent diabetic with cholecystitis takes NPH insulin: 20U AM, 12U PM. After meal developed right subcostal pain, nausea, vomiting, sleepiness, increased polyuria. Best prehospital measure for crisis prevention?",
      options: {
        A: "Change insulin regimen",
        B: "Take analgesics",
        C: "Exclude fats from diet",
        D: "Take cholagogues",
        E: "Decrease carbohydrates in diet"
      },
      correctAnswer: "A",
      explanation: "Symptoms suggest developing diabetic ketoacidosis; immediate insulin regimen adjustment is needed to prevent crisis."
    }
,
    {
      id: 33,
      question: "Surgery unit received person with incised stab wound on upper third of right thigh 3.0x0.5x2.0 cm. Bright-red blood flows from deep within in pulsing stream. Characterize this bleeding type:",
      options: {
        A: "Parenchimatous",
        B: "Arterial",
        C: "Venous",
        D: "Mixed",
        E: "Capillary"
      },
      correctAnswer: "B",
      explanation: "Bright red blood flowing in a pulsatile stream indicates arterial bleeding."
    },
    {
      id: 34,
      question: "A 13-year-old girl complains of dyspnea and shin/foot edemas after physical exertion for two weeks. Edemas decrease in morning. Exam shows enlarged liver and coarse systolic murmur. Blood and urine normal. Most likely cause of edemas?",
      options: {
        A: "Angioneurotic edema",
        B: "Hepatic cirrhosis",
        C: "Nephrotic syndrome",
        D: "Heart failure",
        E: "Acute pyelonephritis"
      },
      correctAnswer: "D",
      explanation: "Exercise-induced dyspnea with dependent edema that improves with rest, along with systolic murmur, indicates heart failure."
    },
    {
      id: 35,
      question: "A district doctor diagnosed one of his patients with dysentery. What accounting document reflects this type of morbidity?",
      options: {
        A: "Urgent report",
        B: "Certificate of temporary disability",
        C: "Statistical report",
        D: "Report on major non-epidemic disease",
        E: "Control card of registered patient"
      },
      correctAnswer: "A",
      explanation: "Dysentery is a notifiable disease requiring immediate reporting through an urgent notification system."
    },
    {
      id: 36,
      question: "During hiring, a prospective employee underwent preventive medical examination and was declared fit to work. What type of preventive medical examination was it?",
      options: {
        A: "Specific",
        B: "Scheduled",
        C: "Preliminary",
        D: "Comprehensive",
        E: "Periodical"
      },
      correctAnswer: "C",
      explanation: "A pre-employment medical examination is classified as a preliminary preventive examination."
    },
    {
      id: 37,
      question: "Woman with atopic asthma found to have dog hair allergen +++. Despite removing carpets, renovation, air conditioning, and pathogenetic therapy, nightly attacks continue. What long-term treatment can decrease allergen sensitivity?",
      options: {
        A: "Specific hyposensitization",
        B: "Continuation of prior treatment",
        C: "Antihistamine therapy",
        D: "Buteyko breathing technique",
        E: "Referral for speleotherapy"
      },
      correctAnswer: "A",
      explanation: "Specific allergen immunotherapy (hyposensitization) is the only treatment that can modify the underlying allergic response."
    },
    {
      id: 38,
      question: "A 45-year-old woman with Werlhof disease has: Hb 100 g/L, platelets 90·109/L. Single small thigh hematoma after stumbling. What treatment tactics?",
      options: {
        A: "Administer thrombocytic mass, continue in hematology",
        B: "Urgent hospitalization into general care",
        C: "Continue supervision by hospital hematologist",
        D: "Urgent hospitalization into hematology"
      },
      correctAnswer: "C",
      explanation: "With stable platelet count and minor symptoms, continued outpatient monitoring is appropriate."
    },
    {
      id: 39,
      question: "Human body receives chemicals from atmosphere. What type of action results in combined effect less than sum of isolated effects?",
      options: {
        A: "Potentiation",
        B: "Antagonism",
        C: "Synergistic action",
        D: "Complex action",
        E: "Isolated action"
      },
      correctAnswer: "B",
      explanation: "Antagonism occurs when the combined effect of chemicals is less than the sum of their individual effects."
    },
    {
      id: 40,
      question: "A 10-year-old boy with arthritis and myocarditis was diagnosed with juvenile rheumatoid arthritis. What symptom is most contributive for diagnosis?",
      options: {
        A: "Increased heart rate",
        B: "Reduced mobility of joints in morning",
        C: "Enlarged heart",
        D: "Affection of large joints",
        E: "Regional hyperemia of joints"
      },
      correctAnswer: "B",
      explanation: "Morning stiffness with reduced joint mobility is the most characteristic diagnostic feature of juvenile rheumatoid arthritis."
    }
,
    {
      id: 41,
      question: "A woman has been provisionally diagnosed with pheochromocytoma. BP normal at intermission, tendency towards tachycardia. No urine pathologies. Decision made to perform provocative test with histamine. What drug should be kept for emergency aid if test positive?",
      options: {
        A: "Phentolamine",
        B: "Prednisolone",
        C: "Pipolphen (Promethazine)",
        D: "Nifedipine",
        E: "Mesaton (Phenylephrine)"
      },
      correctAnswer: "A",
      explanation: "Phentolamine, an alpha-blocker, is essential for managing potential hypertensive crisis during histamine provocation test in pheochromocytoma."
    },
    {
      id: 42,
      question: "A 50-year-old patient presented with blood in urine. Urination painless and undisturbed. Has had macrohematuria for 3 days. Kidneys cannot be palpated, suprapubic area normal. Prostate normal on exam. Cystoscopy shows no changes. Most likely diagnosis?",
      options: {
        A: "Necrotic papillitis",
        B: "Dystopic kidney",
        C: "Varicocele",
        D: "Bladder tuberculosis",
        E: "Renal carcinoma"
      },
      correctAnswer: "E",
      explanation: "Painless gross hematuria in older adult with normal lower urinary tract exam suggests renal cell carcinoma until proven otherwise."
    },
    {
      id: 43,
      question: "A 30-year-old woman during regular gynecological examination was found to have dark blue 'punctulated perforations' on the vaginal portion of the uterine cervix. The doctor suspects endometriosis of the vaginal portion of the uterine cervix. Most informative investigation method?",
      options: {
        A: "Colposcopy, target biopsy of the cervix",
        B: "Curettage of the uterine cavity",
        C: "Hormone testing",
        D: "US of the lesser pelvis",
        E: "Hysteroscopy"
      },
      correctAnswer: "A",
      explanation: "Colposcopy with targeted biopsy is the gold standard for confirming cervical endometriosis and evaluating suspicious cervical lesions."
    },
    {
      id: 44,
      question: "A woman has been working as a polisher for 1.5 years with grinding machine. Complains of white finger discoloration when nervous. No visible changes. Grip strength 25kg. Cold stimulus extremely positive on limbs. Internal organs normal. Diagnosis?",
      options: {
        A: "Polyneuritis",
        B: "Syringomyelia",
        C: "Vibration disease",
        D: "Raynaud syndrome",
        E: "Raynaud disease"
      },
      correctAnswer: "C",
      explanation: "Occupational exposure to vibration with characteristic vasospastic symptoms indicates vibration disease/hand-arm vibration syndrome."
    },
    {
      id: 45,
      question: "A 28-year-old man complains of skin rash and itching on both hands for 1.5 years. Exacerbation relates to occupational contact with formaldehyde resins. Lesions show erythema, papules, vesicles, erosions, crusts. Most likely diagnosis?",
      options: {
        A: "Simple contact dermatitis",
        B: "Allergic dermatitis",
        C: "Idiopathic eczema",
        D: "Erythema multiforme",
        E: "Occupational eczema"
      },
      correctAnswer: "E",
      explanation: "The chronic nature, clear occupational exposure trigger, and characteristic polymorphic lesions indicate occupational eczema."
    },
    {
      id: 46,
      question: "A 13-year-old boy has severe pulmonary mucoviscidosis. Complains of dyspnea and blood expectoration. Shows lagging development, acrocyanosis, hepatomegaly, drumstick fingers. Suspected chronic pulmonary heart disease. Most informative examination?",
      options: {
        A: "Doppler echocardiography",
        B: "Electrocardiography",
        C: "Chest X-ray",
        D: "Rheography of pulmonary artery",
        E: "Ultrasound of liver"
      },
      correctAnswer: "A",
      explanation: "Doppler echocardiography is most informative for evaluating right heart function and pulmonary hypertension in cor pulmonale."
    },
    {
      id: 47,
      question: "A 38-year-old woman after physical exertion suddenly developed palpitations, dyspnea, dull cardiac pain. Has rheumatic heart disease history. Pulse unequal, 96/min. BP 110/70mmHg, HR 120/min. ECG shows uneven waves instead of P-waves, irregular R-R. Most likely diagnosis?",
      options: {
        A: "Atrial flutter",
        B: "Paroxysmal supraventricular tachycardia",
        C: "Paroxysmal ventricular tachycardia",
        D: "Respiratory arrhythmia",
        E: "Atrial fibrillation"
      },
      correctAnswer: "E",
      explanation: "The irregular pulse, absence of P waves replaced by fibrillation waves, and unequal R-R intervals in rheumatic heart disease patient indicate atrial fibrillation."
    },
    {
      id: 48,
      question: "A 36-year-old man complains of dyspnea and cardiac pain after flu 2 weeks ago. Shows swollen cyanotic face, distended neck veins. Extended heart borders, muffled sounds, HR=Pulse=118/min, BP 90/60mmHg. ECG: low voltage. X-ray: trapezoidal heart. Best treatment?",
      options: {
        A: "Glucocorticosteroids",
        B: "Antibiotics",
        C: "Pericardectomy",
        D: "Diuretics",
        E: "Pericardial puncture"
      },
      correctAnswer: "E",
      explanation: "Signs of cardiac tamponade following viral pericarditis require immediate pericardiocentesis to prevent hemodynamic collapse."
    },
    {
      id: 49,
      question: "A 51-year-old alcoholic complains of blood vomiting. First jaundiced at 40. Shows jaundice, spider angiomas, malnutrition, ascites. Liver +3cm, spleen +2cm. Blood: Hb 80g/L, WBC 3·109/L, platelets 85·109/L. Cause of portal hypertension?",
      options: {
        A: "Constrictive pericarditis",
        B: "Hemochromatosis",
        C: "Splenic vein thrombosis",
        D: "Budd-Chiari syndrome",
        E: "Hepatic cirrhosis"
      },
      correctAnswer: "E",
      explanation: "History of alcoholism, physical findings of cirrhosis (jaundice, spider angiomas, ascites), and pancytopenia indicate alcoholic cirrhosis as cause of portal hypertension."
    },
    {
      id: 50,
      question: "A 7-year-old boy with severe cystic fibrosis has dyspnea and hemoptysis. Shows poor growth, acrocyanosis, hepatomegaly, clubbing. Suspected cor pulmonale. Most informative confirmatory test?",
      options: {
        A: "Doppler echocardiography",
        B: "Electrocardiography",
        C: "Chest X-ray",
        D: "Pulmonary artery rheography",
        E: "Liver ultrasound"
      },
      correctAnswer: "A",
      explanation: "Doppler echocardiography is most informative for evaluating pulmonary hypertension and right heart function in cor pulmonale secondary to cystic fibrosis."
    }
  ];

  const handleSubmit = (selectedOption) => {
    if (!answered) {
      setUserAnswer(selectedOption);
      setAnswered(true);
      if (selectedOption === questions[currentQuestion].correctAnswer) {
        setScore(score + 1);
      }
      saveAnswer();
    }
  };

  const nextQuestion = () => {
    if (currentQuestion < questions.length - 1) {
      setCurrentQuestion(currentQuestion + 1);
      setShowAnswer(false);
      setAnswered(false);
      setKeyword('');
      setExplanation('');
      setUserAnswer('');
    } else {
      setShowResults(true);
    }
  };

  const downloadResults = () => {
    const csvContent = [
      ['Question ID', 'Question', 'Student Keywords', 'Student Explanation', 'Selected Answer', 'Correct Answer', 'Is Correct'],
      ...studentAnswers.map(answer => [
        answer.questionId,
        answer.question,
        answer.keywords,
        answer.studentExplanation,
        answer.selectedAnswer,
        answer.correctAnswer,
        answer.isCorrect
      ])
    ]
    .map(row => row.map(str => `"${str}"`).join(','))
    .join('\n');

    const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
    const link = document.createElement('a');
    const url = URL.createObjectURL(blob);
    link.setAttribute('href', url);
    link.setAttribute('download', 'quiz_results.csv');
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
  };

  return (
    <div className="max-w-4xl mx-auto p-4">
      <Card>
        <CardHeader>
          <CardTitle className="text-2xl font-bold">Medical Quiz Game</CardTitle>
          <div className="text-lg">Score: {score}/{questions.length}</div>
        </CardHeader>
        <CardContent>
          <div className="space-y-6">
            {/* Pre-answer inputs */}
            <div className="space-y-4">
              <div>
                <label className="block text-sm font-medium mb-2">Key Words:</label>
                <input
                  type="text"
                  className="w-full p-2 border rounded"
                  value={keyword}
                  onChange={(e) => setKeyword(e.target.value)}
                  placeholder="Enter key words for this question..."
                />
              </div>
              <div>
                <label className="block text-sm font-medium mb-2">Your Explanation:</label>
                <textarea
                  className="w-full p-2 border rounded"
                  value={explanation}
                  onChange={(e) => setExplanation(e.target.value)}
                  placeholder="Write your understanding of the question..."
                  rows={3}
                />
              </div>
            </div>

            {/* Question */}
            <div className="my-4">
              <h3 className="text-lg font-semibold">Question {currentQuestion + 1}:</h3>
              <p className="my-2">{questions[currentQuestion].question}</p>
            </div>

            {/* Options */}
            <div className="space-y-2">
              {Object.entries(questions[currentQuestion].options).map(([key, value]) => (
                <button
                  key={key}
                  onClick={() => handleSubmit(key)}
                  className={`w-full p-3 text-left rounded ${
                    answered
                      ? key === questions[currentQuestion].correctAnswer
                        ? 'bg-green-100'
                        : key === userAnswer
                        ? 'bg-red-100'
                        : 'bg-gray-50'
                      : 'bg-gray-50 hover:bg-gray-100'
                  }`}
                  disabled={answered}
                >
                  <span className="font-bold">{key}:</span> {value}
                  {answered && key === questions[currentQuestion].correctAnswer && (
                    <Check className="inline ml-2 text-green-500" />
                  )}
                  {answered && key === userAnswer && key !== questions[currentQuestion].correctAnswer && (
                    <X className="inline ml-2 text-red-500" />
                  )}
                </button>
              ))}
            </div>

            {/* Answer explanation */}
            {answered && (
              <Alert>
                <AlertDescription>
                  {questions[currentQuestion].explanation}
                </AlertDescription>
              </Alert>
            )}

            {/* Next button */}
            {answered && currentQuestion < questions.length - 1 && (
              <button
                onClick={nextQuestion}
                className="mt-4 px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600 flex items-center"
              >
                Next Question <ArrowRight className="ml-2" />
              </button>
            )}
          </div>
        </CardContent>
      </Card>
    </div>
  );
};

export default QuizGame;
