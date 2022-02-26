#Download all of the english language .txt files from Project Gutenberg
wget -m -H "http://www.gutenberg.org/robot/harvest?filetypes[]=txt&langs[]=en"

#Get rid of all of the duplicate encodings in ISO-<something> and UTF-8.
find . -name "*-8.zip" | xargs rm
find . -name "*-0.zip" | xargs rm

# Remove other random stuff at the recommendation of https://gist.github.com/mbforbes/cee3fd5bb3a797b059524fe8c8ccdc2b
find . -name "89-AnnexI.zip" | xargs rm
find . -name "89-Descriptions.zip" | xargs rm
find . -name "89-Contents.zip" | xargs rm
find . -name "3290-u.zip" | xargs rm
find . -name "5192-tex.zip" | xargs rm
find . -name "10681-index.zip" | xargs rm
find . -name "10681-body.zip" | xargs rm
find . -name "13526-page-inames.zip" | xargs rm
find . -name "15824-h.zip" | xargs rm
find . -name "18251-mac.zip" | xargs rm


#Unzip all of the files recursively with multi-core xargs (-P 5)
find . -name "*.zip" | xargs -P 5 -I fileName sh -c 'unzip -o -d "$(dirname "fileName")/$(basename -s .zip "fileName")" "fileName"'

#Find all of the .txt files (and .TXT files!) and move them to a folder called /textonly
find . -iname "*.txt" -exec mv {} ./textonly \;
