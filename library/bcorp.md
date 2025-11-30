# Description
  
According to [their website](https://www.bcorporation.net/en-us/certification):

> B Corp Certification is a designation that a business is meeting high standards of verified performance, accountability, and transparency on factors from employee benefits and charitable giving to supply chain practices and input materials. In order to achieve certification, a company must: 
>
>  - Demonstrate high social and environmental performance by achieving a B Impact Assessment score of 80 or above and passing our risk review. Multinational corporations must also meet baseline requirement standards. 
>
>  - Make a legal commitment by changing their corporate governance structure to be accountable to all stakeholders, not just shareholders, and achieve benefit corporation status if available in their jurisdiction. 
>
>  - Exhibit transparency by allowing information about their performance measured against B Lab’s standards to be publicly available on their B Corp profile on B Lab’s website.  

# Data sources

B Corp provides a nice web-based user interface to browse certified companies.

Digging thought the FAQ allows us to find
[a link to Data.World](https://data.world/blab/b-corp-impact-data)
where they provide a list of present and past certified corporations in a file in CSV format.
The data set is updated several times per year.
  
# How we use their data
  
B Corp certifies not individual products but whole companies.
The only entry in their data set that allows us to reliably connect it to other databases is the corporations website link.
From the links we extract the domain and try to match it with entries in Wikidata.

All products of matched companies have higher chances to be shown as alternative products in a our product view.

