# arxiv_mining
I've established the repos as a temporary resting place for data extracted from arxiv using the p2t API. At least initially, you should find a file called result.json, the results of applying the p2t bbox and simple-scatter-plot API methods to all pdf pages in the initial tar volume available for arxiv, arXiv_pdf_0001_001.tar

If you peek at these records, each element in the array gives some json describing:

i) the input document, specifically the arxiv URL (as per the policy for working with arxi pdfs, found here : https://arxiv.org/help/bulk_data_s3)
ii) the page that the result comes from, specifically an image of the page
iii) the JSON data file extracted from the region of the page, which corresponds to x-y values inverted from the scaling information found in the image
iv) the input bounding box region extracted from the page, and lastly
v) an image showing the fit produced by the simple-scatter-plot API method eg., the locations whose index value corresponds to the position of the corresponding x-y values in the output JSON

one such element of result.json looks like: 

{
"url":"http://arxiv.org/abs/astro-ph/0001003",
"page":"outputs/astro-ph0001003-000005.png",
"data":"outputs/e154b55290bc2eea70f5a226806c2072.json",
"input":"outputs/e154b55290bc2eea70f5a226806c2072_in.png",
"fit":"outputs/e154b55290bc2eea70f5a226806c2072_out.png"
}

If you wanted to import this complete array into mongo DB (for example) , you could issue: 

mongoimport --db dbName --collection collectionName --file result.json --jsonArray

Last but not least, a selection of the output images is available in the file arXiv_pdf_0001_001_text_out.tar.gz and the text extraction results are available in arXiv_pdf_0001_001_text_out.tar.gz. 
