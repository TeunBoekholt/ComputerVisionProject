# Computer Vision Project 2 – Joint Detection of AI-Generated Images and Post-Processing Alterations in Real-World Scenarios

**Contributors:** *Anja Skrlj, Filippo Zanei, Teun Boekholt*

---

## 🔗Important Links

> **Google Colab:** [Access Notebook](https://colab.research.google.com/drive/1GE1rqHo-4aLoQ8_zckuA9ZyNcMFjd7ws?usp=sharing)  
> **RDDataset:** [Download via Zenodo](https://zenodo.org/records/14963880)  
> **Project presentation:** [View Slides](https://docs.google.com/presentation/d/1IC4dgNG-5jA0MuH9X87ywiNTE69b9fnXuI8xNbgaCyc/edit?usp=sharing)  

---

## Project Overview

In this project we propose a technique for improving the detection of AI generated images, even when these images have undergone various transformations – redigitalization and being transferred over social media (facebook, instagram, etc. ). In this [original study](https://arxiv.org/pdf/2509.09172) – which has developed the dataset containing transformed real and AI-generated images – the researchers found that existing techniques for detecting AI-generated images often struggle when images have been transformed. 

Therefore, in this project we propose using a DIRE map in combination with a modified classic ResNet-50 architecture to see if this adapted setup performs better when classifying the images from the RDDataset (the name of the dataset from the original study). A DIRE map is an image 'representation' which is retrieved by essentially noising and denoising an image using a diffusion model, and then seeing if the retrieved image is close to the original image. In case it is, the DIRE (DIffusion Reconstruction Error) will be low and we assume the image to have originally be AI-generated – as the DIRE paper's authors pose it, this is under the assumption that AI-generated images will be easier to reconstruct than original image, which is illustrated in the figure below. 

<img width="401" height="382" alt="Scherm­afbeelding 2026-06-12 om 15 33 36" src="https://github.com/user-attachments/assets/e80a412e-755b-42f5-a32d-4b9e11b7ef46" />


Because generating DIRE maps and training on all 52.000 images included in the RDDataset is extremely costly and outside the capacity of the resources available to us, we decided to train our model only on specific subsets of the data. We experimented with different sizes of subsets to see its effect on our classifier's performance. Since the real image category in the dataset does not contain categorical labels, we opted for subsets of randomaly retrieved images from the RDDataset, evenly split among AI-generated and real images, but not picked from any specific category within the AI-generated class.

---

## Run Guide

Running our notebook should be self-explanatory following the comments within. 

**Important Note:** Importing the dataset from our shared Google Drive folder, just like the generation of the DIRE maps, is very costly and unnecesary. The DIRE maps used for our experiments have already been saved in another Drive folder and can – using the provided code – directly be imported from there. These DIRE maps can then be used in the 'Train' and 'Test' sections to train our modified ResNet-50 model and to evaluate it. 

In case a full reproduction of our process has to be carried out, a shortcut to the shared Drive folder containing the entire (and subsets of) the RDDatset should be added to the Google Drive of the account executing the notebook. Further instruction on how to do this are included in the Colab Notebook itself.
