# scoreAI

The code provided here is serves as supplementary material to the paper:

* Wardell, V., Esposito, C. L., Madan, C. R., & Palombo, D. J. (preprint). Semi-automated transcription and scoring of autobiographical memory narratives.

The code has been written by Christopher Madan, with consultation of the other authors.

A set of three example transcribed and scored memories are provided to demonstrate how a memory document should be formatted. These memories are from one of the researchers, not a study participant. We do not share narratives from participants for privacy reasons. We also demonstrate that text can be visually ‘redacted’ by highlighting it in black; this is also shown in the example, but note that the original text is still maintained (as in the redacted dates in the example). A blank template of the format used here, and required by the Python code, is also provided.

Current public version: build 9 [20200207]

## Installation Instructions

The Python script should run on any system capable of running Python 3.x. For new users we recommend installing Python via the Anaconda distribution [https://www.anaconda.com/distribution/]. The code also requires the python-docx package [https://python-docx.readthedocs.io/en/latest/user/install.html], which is available in pip.

`pip install python-docx`

## Usage

The function of the Python script is described in Appendix B of the paper.

The first section requires the user to configure the code and should be adjusted on a case-by-case basis. The options to configure include specifying the directory that has the input Word documents, the folder to output the stacked data to, and the number of memories in each Word document. The specific filename of the Word documents does not matter, though the script will load the files in alphabetical order and assumes no other files are in this input directory. Each Word document is expected to have the number of memories configured and be formatted as specified in the template. For an example of a scored memory document, see `example_scoring.docx`.

The second section and onwards should not be modified unless changing the overall functionality of the script (e.g., using a different document template or changing the memory labels. The second section of the code loads several Python modules into the environment for the script to use in the processing of the documents. The only non-standard Python module that is required is python-docx, which can be installed using the pip program (see https://python-docx.readthedocs.io/en/latest/user/install.html). 

The third section defines the memory scoring labels (e.g., `Int_EV`, `Ext_SEM`), looks up the list of files in the input directory, and includes additional ‘under the hood’ settings. 

The fourth and fifth section do most of the actual work. The fourth section defines several functions that will need to be used repeatedly, such as for extracting specific paragraphs of text from the document and counting the number of occurrences for each scoring label. The fifth section of code brings it all together, cycling through each document, first extracting the participant ID and episodic richness ratings. The code then goes through and finds the start of each memory within the document and then uses these to extract the related text and calculate the component memory scores. These scores are then converted into a single data record along with the participant ID and episodic richness values, such that each memory is it’s own row. This then continues until all of the documents are processed and iteratively merged together. The final section of code convert these records into a dataframe format and then outputs them as a CSV into the designated output folder, with the filename including the number of documents (i.e., number of participants) and current date. An example output file, corresponding to the example scored memory document, is provided as `example_output.csv`.

## License

The code is released under a GNU GPL v3 license. See `LICENSE` for further details.
