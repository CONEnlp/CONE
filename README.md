## Environment
The experiment is set with Python 3.8.5 and cuda11.1. Dependency packages are in requirement.txt, you could use `pip` to install:

```{bash}
(envforcone)$ pip install -r requirements.txt
```

## Data
CONE uses data from HotelRec(https://github.com/Diego999/HotelRec) and VAD(https://github.com/somethingx1202/VADet).


## Preprocessing
Preprocessed data for HotelRec in [data/hotel/]:
```{bash}
(envforcone)$ python clean_hotel.py
(envforcone)$ python aug_translate.py
```
Similar for VAD.

To include a customized data set, first create a repo `data/{dataset_name}/clean`. The
following four files must be inside this folder:

* `reviews.txt`: a `[num_sentences]` -length file where each line being
  one sentence in the corpus.
* `reviews_aug_tran.txt`: a `[num_sentences]` -length file where each line being
  the corresponding augmented sentence.
* `sentiments.npy`: a `[num_sentences]` -length file where each line denotes
  the corresponding sentiment pseudo label.

The following files can be inside this folder if available:
* `document_rating.npy`: a `[num_document]` -length file where each line denotes
  the corresponding sentiment label.
* `documents.npy`: a `[num_sentences]` -length file where each line denotes
  the corresponding document index.
* `hotels.npy`: a `[num_sentences]` -length file where each line denotes
  the corresponding hotel index. 
  Such information could also be other labels, such as user, brand, etc.

## Training & Evaluation
Run CONE.py with the command:
```{bash}
(envforcone)$ python CONE.py --to_evaluate "true"
```

## Example output
HotelRec:
* *{'aspectsplit': 0.03829713493530499, 'sentimentsplit': {0: {'percentage': 0.92, 'keypoint': ['These go at least every  seconds around the building and are incredibly noisy to the point where the room shakes.\n', 'One of our rooms was directly facing the outdoor stage where the band performed every night...LOUDLY.\n', 'What was supposed to be a quiet break left me exhausted!!!!!!!\n']}, 1: {'percentage': 0.08, 'keypoint': ['Once you were inside it was really quiet, I think being out the back was a good thing.\n', 'I was in , quite quiet and a good size too.\n', 'Everything was in walking distance but not under your nose so it was quiet most of the time!\n']}}}*

VAD:
* *{'aspectsplit': 0.042033920940170943, 'sentimentsplit': {0: {'percentage': 0.18, 'keypoint': ['A CANADIAN federal panel NACI that has advised the feds since 1964 on vaccine issues that expressed the findings concerning the AstraZeneca vaccine but sure dumbass , flail away about other countries while accussing Opposition of stoking fear . #cdnpoli #canpoli\n', "Nearly 400000 AstraZeneca Vaccine Doses Seized in Italy After Teacher’s Death BY JACK PHILLIPS March 15 , 2021 Updated : March 15 , 2021 Covid Beware : Research It's Your Life\n", '“The Biden administration is refusing to allow AstraZeneca to export tens of millions of unused doses of its COVID19 vaccine , despite a plea from the Canadian government to import the shots in a bid to bolster Ottawa’s lagging inoculation drive . #cdnpoli\n']}, 1: {'percentage': 0.82, 'keypoint': ['BREAKING : Health Canada greenlights U . S . batch of AstraZeneca COVID19 vaccine #cdnpoli\n', 'BREAKING U . S . plans to send 1 . 5M doses of AstraZeneca COVID19 vaccine to Canada : report #cdnpoli\n', 'The Biden admin is considering sending some AstraZeneca Covid19 vaccine doses stockpiled waiting for official usage approval in the US over the border to Mexico Canada , per a sr admin official . They may propose a swap agreement , story :\n']}}}*
