# Search files using the fastest Regex Engine ever - ripgrep - replacement is also supported!

Uses https://github.com/BurntSushi/ripgrep and parses the regular expression output into a pandas DataFrame.
It is much faster than the first version: https://github.com/hansalemaos/PYRipGREP due to more efficient parsing, and substitution is 
also supported (BACK UP YOUR DATA BEFORE!). Check out the examples 

### Tested against Windows 10 / Python 3.10 / Anaconda 


## pip install rushex

```python
import random

from rushex import FullBore


monsterregex = FullBore(ripgrepexe=r"rg.exe") 


files = [
    r"C:\testxt\xab.txt",
    r"C:\testxt\ö.txt",
    r"C:\testxt\xaa.txt",
    r"C:\testxt\xaa2.txt",
    r"C:\testxt\pypigitupload.py",
    r"C:\testxt\pyripbro.py",
    r"C:\testxt\pip2dfxxxxxxxxx.py",
]
dfa = monsterregex.find_all_in_files(
    regular_expressions=[
        r"\b\w{15}\b",
        r"\b\d{4}\b",
    ],  # pass as many regular expressions as you want
    files=files,
    ignore_case=True,
    allowed_extensions=(),  # if empty, no file ending is excluded
    binary=True,
    dfa_size="1G",
    multiline=False,
    multiline_dotall=False,
    field_match_separator="ÇÇÇÇÇ",
)  # A string which won't show up in your search results

# print(dfa[:5].to_string())
#                     aa_filename  aa_line  aa_byte_offset_o     aa_string_bytes  aa_byte_len        aa_string aa_replacement                aa_newfilename
# 0  C:\testxt\pip2dfxxxxxxxxx.py        1               589  b'ignore_packages'           15  ignore_packages            b''  C:\testxt\pip2dfxxxxxxxxx.py
# 1  C:\testxt\pip2dfxxxxxxxxx.py        1               650  b'ignore_packages'           15  ignore_packages            b''  C:\testxt\pip2dfxxxxxxxxx.py
# 2  C:\testxt\pip2dfxxxxxxxxx.py        1               694  b'ignore_packages'           15  ignore_packages            b''  C:\testxt\pip2dfxxxxxxxxx.py
# 3  C:\testxt\pip2dfxxxxxxxxx.py        1               731  b'ignore_packages'           15  ignore_packages            b''  C:\testxt\pip2dfxxxxxxxxx.py
# 4  C:\testxt\pip2dfxxxxxxxxx.py        1              1126  b'ignore_packages'           15  ignore_packages            b''  C:\testxt\pip2dfxxxxxxxxx.py

df3 = monsterregex.find_all_in_folders(
    folders=[r"C:\ProgramData\anaconda3\envs\adda"],
    regular_expressions=[r"\bnumexpr|pandas\b", r"\bnp\b."],
    allowed_extensions=(".py",),  # searches only in py files
    ignore_case=True,
    maxsubfolders=-1,  # all subfolders
)

# print(df3[:5].to_string())
#                                                  aa_filename  aa_line  aa_byte_offset_o aa_string_bytes  aa_byte_len aa_string aa_replacement                                             aa_newfilename
# 0  C:\ProgramData\anaconda3\envs\adda\winrtocrxxxxxxxxxxx.py        1                 7       b'pandas'            6    pandas            b''  C:\ProgramData\anaconda3\envs\adda\winrtocrxxxxxxxxxxx.py
# 1  C:\ProgramData\anaconda3\envs\adda\winrtocrxxxxxxxxxxx.py        1               135       b'pandas'            6    pandas            b''  C:\ProgramData\anaconda3\envs\adda\winrtocrxxxxxxxxxxx.py
# 2           C:\ProgramData\anaconda3\envs\adda\rushextest.py        1              1173       b'pandas'            6    pandas            b''           C:\ProgramData\anaconda3\envs\adda\rushextest.py
# 3           C:\ProgramData\anaconda3\envs\adda\rushextest.py        1              1433       b'pandas'            6    pandas            b''           C:\ProgramData\anaconda3\envs\adda\rushextest.py
# 4           C:\ProgramData\anaconda3\envs\adda\rushextest.py        1              1690       b'pandas'            6    pandas            b''           C:\ProgramData\anaconda3\envs\adda\rushextest.py
df4 = monsterregex.find_all_in_folders(
    folders=[r"C:\ProgramData\anaconda3\envs\adda"],
    regular_expressions=[r"\bnumexpr|pandas\b", r"\bnp\.\b"],
    allowed_extensions=(),
    ignore_case=True,
    maxsubfolders=-1,
)
#                                                                 aa_filename  aa_line  aa_byte_offset_o aa_string_bytes  aa_byte_len aa_string aa_replacement                                                            aa_newfilename
# 0       C:\ProgramData\anaconda3\envs\adda\__pycache__\wocr.cpython-310.pyc      222               904       b'pandas'            6    pandas            b''       C:\ProgramData\anaconda3\envs\adda\__pycache__\wocr.cpython-310.pyc
# 1  C:\ProgramData\anaconda3\envs\adda\__pycache__\pdmemedit.cpython-310.pyc      515              3496          b'np.'            3       np.            b''  C:\ProgramData\anaconda3\envs\adda\__pycache__\pdmemedit.cpython-310.pyc
# 2  C:\ProgramData\anaconda3\envs\adda\__pycache__\pdmemedit.cpython-310.pyc     1318              8867       b'pandas'            6    pandas            b''  C:\ProgramData\anaconda3\envs\adda\__pycache__\pdmemedit.cpython-310.pyc
# 3  C:\ProgramData\anaconda3\envs\adda\__pycache__\pdmemedit.cpython-310.pyc     1318              9327       b'pandas'            6    pandas            b''  C:\ProgramData\anaconda3\envs\adda\__pycache__\pdmemedit.cpython-310.pyc
# 4  C:\ProgramData\anaconda3\envs\adda\__pycache__\pdmemedit.cpython-310.pyc     2827             15327      b'numexpr'            7   numexpr            b''  C:\ProgramData\anaconda3\envs\adda\__pycache__\pdmemedit.cpython-310.pyc
df5 = monsterregex.find_all_in_folders(
    folders=[r"C:\ProgramData\anaconda3\envs\adda"],
    regular_expressions=[r"\bnumexpr|pandas\b", r"\bnp\b."],
    allowed_extensions=(".py",),
    ignore_case=True,
    maxsubfolders=2,
    binary=False,
    dfa_size="100M",
    multiline=False,
    multiline_dotall=False,
    field_match_separator="ÇÇÇÇÇ",
)
#                                                  aa_filename  aa_line  aa_byte_offset_o aa_string_bytes  aa_byte_len aa_string aa_replacement                                             aa_newfilename
# 0  C:\ProgramData\anaconda3\envs\adda\winrtocrxxxxxxxxxxx.py        1                 7       b'pandas'            6    pandas            b''  C:\ProgramData\anaconda3\envs\adda\winrtocrxxxxxxxxxxx.py
# 1  C:\ProgramData\anaconda3\envs\adda\winrtocrxxxxxxxxxxx.py        1               135       b'pandas'            6    pandas            b''  C:\ProgramData\anaconda3\envs\adda\winrtocrxxxxxxxxxxx.py
# 2           C:\ProgramData\anaconda3\envs\adda\rushextest.py        1              1173       b'pandas'            6    pandas            b''           C:\ProgramData\anaconda3\envs\adda\rushextest.py
# 3           C:\ProgramData\anaconda3\envs\adda\rushextest.py        1              1433       b'pandas'            6    pandas            b''           C:\ProgramData\anaconda3\envs\adda\rushextest.py
# 4           C:\ProgramData\anaconda3\envs\adda\rushextest.py        1              1690       b'pandas'            6    pandas            b''           C:\ProgramData\anaconda3\envs\adda\rushextest.py
df6 = monsterregex.find_all_in_folders(
    folders=[r"C:\ProgramData\anaconda3\envs\adda"],
    regular_expressions=[r"\bnp\b.*?\bpd\b"],
    allowed_extensions=(".py",),
    ignore_case=True,
    maxsubfolders=-1,
    binary=False,
    dfa_size="100M",
    multiline=True,
    multiline_dotall=True,
    field_match_separator="ÇÇÇÇÇ",
)
# print(df5[:6].to_string())
#                                                  aa_filename  aa_line  aa_byte_offset_o aa_string_bytes  aa_byte_len aa_string aa_replacement                                             aa_newfilename
# 0  C:\ProgramData\anaconda3\envs\adda\winrtocrxxxxxxxxxxx.py        1                 7       b'pandas'            6    pandas            b''  C:\ProgramData\anaconda3\envs\adda\winrtocrxxxxxxxxxxx.py
# 1  C:\ProgramData\anaconda3\envs\adda\winrtocrxxxxxxxxxxx.py        1               135       b'pandas'            6    pandas            b''  C:\ProgramData\anaconda3\envs\adda\winrtocrxxxxxxxxxxx.py
# 2           C:\ProgramData\anaconda3\envs\adda\rushextest.py        1              1173       b'pandas'            6    pandas            b''           C:\ProgramData\anaconda3\envs\adda\rushextest.py
# 3           C:\ProgramData\anaconda3\envs\adda\rushextest.py        1              1433       b'pandas'            6    pandas            b''           C:\ProgramData\anaconda3\envs\adda\rushextest.py
# 4           C:\ProgramData\anaconda3\envs\adda\rushextest.py        1              1690       b'pandas'            6    pandas            b''           C:\ProgramData\anaconda3\envs\adda\rushextest.py
# 5           C:\ProgramData\anaconda3\envs\adda\rushextest.py        1              2528       b'pandas'            6    pandas            b''           C:\ProgramData\anaconda3\envs\adda\rushextest.py


# You can search and replace with rushex

# Get a DataFrame
df7 = monsterregex.find_all_in_folders(
    folders=[r"C:\grepte\homepagesavetest13", r"C:\grepte\homepagesavetest14"],
    regular_expressions=[r"der|die|das"], # Pass only one regular expression when you want to edit files!!! More than one might corrupt your data!
    allowed_extensions=(".txt", ".html"), 
    ignore_case=True,
    maxsubfolders=-1,
    binary=True,
    dfa_size="100M",
    multiline=True,
    multiline_dotall=False,
    field_match_separator="ÇÇÇÇÇ",
)

# In the DataFrame, there are 2 columns for configuring the replacement: [aa_replacement, aa_newfilename]
# The column aa_replacement MUST contain binary data. I created a method to make your life a little easier: FullBore.cb (not mandatory)
# The column aa_newfilename MUST contain the new file name, if the folders don't exist yet, they will be created.
df7.aa_replacement = df7.apply(  # Different dtypes to bytes
    lambda x: FullBore.cb(100)
    + FullBore.cb(random.choice(["Ü", "Ä", "Ö"]))
    + FullBore.cb("-------------")
    + FullBore.cb(x.aa_string_bytes[0]).upper()
    + FullBore.cb(x.aa_string_bytes[1]).lower()
    + FullBore.cb(x.aa_string_bytes[-1]).upper()
    + b"xxxx"
    + FullBore.cb(
        FullBore.cb(str(random.randint(1, 2000000))),
    ),
    axis=1,
)

# This is how the DataFrame looks like when it is ready:
# print(df7[:6].to_string())
#                                                                        aa_filename  aa_line  aa_byte_offset_o aa_string_bytes  aa_byte_len aa_string                           aa_replacement                                                                   aa_newfilename
# 0  C:\grepte\homepagesavetest13\www.duden.de\rechtschreibung\Seniorenwohnheim.html        1              1570          b'DeR'            3       DeR   b'd\xc3\x96-------------DeRxxxx727601'  C:\grepte\homepagesavetest13\www.duden.de\rechtschreibung\Seniorenwohnheim.html
# 1  C:\grepte\homepagesavetest13\www.duden.de\rechtschreibung\Seniorenwohnheim.html        1              2116          b'DeR'            3       DeR  b'd\xc3\x84-------------DeRxxxx1859128'  C:\grepte\homepagesavetest13\www.duden.de\rechtschreibung\Seniorenwohnheim.html
# 2  C:\grepte\homepagesavetest13\www.duden.de\rechtschreibung\Seniorenwohnheim.html        1              2703          b'DeR'            3       DeR   b'd\xc3\x9c-------------DeRxxxx460032'  C:\grepte\homepagesavetest13\www.duden.de\rechtschreibung\Seniorenwohnheim.html
# 3  C:\grepte\homepagesavetest13\www.duden.de\rechtschreibung\Seniorenwohnheim.html        1              5278          b'DeR'            3       DeR  b'd\xc3\x84-------------DeRxxxx1014873'  C:\grepte\homepagesavetest13\www.duden.de\rechtschreibung\Seniorenwohnheim.html
# 4  C:\grepte\homepagesavetest13\www.duden.de\rechtschreibung\Seniorenwohnheim.html        1             18775          b'DeR'            3       DeR   b'd\xc3\x96-------------DeRxxxx335438'  C:\grepte\homepagesavetest13\www.duden.de\rechtschreibung\Seniorenwohnheim.html
# 5  C:\grepte\homepagesavetest13\www.duden.de\rechtschreibung\Seniorenwohnheim.html        1             26052          b'DeR'            3       DeR  b'd\xc3\x84-------------DeRxxxx1839084'  C:\grepte\homepagesavetest13\www.duden.de\rechtschreibung\Seniorenwohnheim.html

# Now you can run the replacement, dryrun defaults True, so it won't do anything to your files yet. Disable dryrun to
# get it gone, but MAKE A BACKUP BEFORE!
monsterregex.sub(df7)
# DRY RUN:
# C:\grepte\homepagesavetest14\www.duden.de\synonyme\fortwuchern.html
# OLD: 	b'DaS'
# NEW: 	b'd\xc3\x9c-------------DaSxxxx981614'
# ----------------------
# DRY RUN:
# C:\grepte\homepagesavetest14\www.duden.de\synonyme\fortwuchern.html
# OLD: 	b'DiE'
# NEW: 	b'd\xc3\x84-------------DiExxxx303843'
# ----------------------
# DRY RUN:
# C:\grepte\homepagesavetest14\www.duden.de\synonyme\fortwuchern.html
# OLD: 	b'DeR'
# NEW: 	b'd\xc3\x9c-------------DeRxxxx1319395'
monsterregex.sub(df7, dryrun=False)

# You can do the same thing with Python variables, but it is much slower than the file based version.
# I recommend using the module "regex" https://pypi.org/project/regex/ when working with Python strings and bytes.

with open(r"C:\all_corpora_filtered_maryfied.txt", mode="rb") as f:
    data = f.read()

datau = data.decode("utf-8", "ignore")


results1 = monsterregex.find_all_in_variable(
    regular_expressions=[r"\bHaus\w+\b"], variable=data
)
```


```python
class FullBore(builtins.object)
 |  FullBore(ripgrepexe: Optional[str] = None, msvc_or_gnu='msvc')
 |  
 |  Methods defined here:
 |  
 |  __init__(self, ripgrepexe: Optional[str] = None, msvc_or_gnu='msvc')
 |      Initializes the FullBore class with the path to the ripgrep executable.
 |      
 |      Args:
 |          ripgrepexe (Union[str, None], optional): Path to the ripgrep executable. Defaults to None.
 |          msvc_or_gnu (str, optional): Compiler to use for installing ripgrep. Defaults to 'msvc'.
 |  
 |  find_all_in_files(self, regular_expressions: Union[list, str], files: Union[list, str], ignore_case: bool = True, allowed_extensions: tuple = (), binary: bool = True, dfa_size: str = '1G', multiline: bool = False, multiline_dotall: bool = False, field_match_separator: str = 'ÇÇÇÇÇ') -> pandas.core.frame.DataFrame
 |      Searches for all regular expressions in the input files.
 |      
 |      Args:
 |          regular_expressions (Union[list, str]): Regular expressions to be searched.
 |          files (Union[list, str]): Input files to be searched.
 |          ignore_case (bool, optional): Ignore case while searching. Defaults to True.
 |          allowed_extensions (tuple, optional): Allowed file extensions. Defaults to ().
 |          binary (bool, optional): Search in binary mode. Defaults to True.
 |          dfa_size (str, optional): DFA size for ripgrep. Defaults to "1G".
 |          multiline (bool, optional): Search in multiline mode. Defaults to False.
 |          multiline_dotall (bool, optional): Search in multiline dotall mode. Defaults to False.
 |          field_match_separator (str, optional): Field match separator. Defaults to "ÇÇÇÇÇ".
 |      
 |      Returns:
 |          pd.DataFrame: Dataframe containing the search results.
 |  
 |  find_all_in_folders(self, regular_expressions: Union[list, str], folders: Union[list, str], ignore_case: bool = True, allowed_extensions: tuple = (), maxsubfolders: int = -1, binary: bool = True, dfa_size: str = '1G', multiline: bool = False, multiline_dotall: bool = False, field_match_separator: str = 'ÇÇÇÇÇ') -> pandas.core.frame.DataFrame
 |      Searches for all regular expressions in the input folders.
 |      
 |      Args:
 |          regular_expressions (Union[list, str]): Regular expressions to be searched.
 |          folders (Union[list, str]): Input folders to be searched.
 |          ignore_case (bool, optional): Ignore case while searching. Defaults to True.
 |          allowed_extensions (tuple, optional): Allowed file extensions. Defaults to ().
 |          maxsubfolders (int, optional): Maximum number of subfolders to be searched. Defaults to -1.
 |          binary (bool, optional): Search in binary mode. Defaults to True.
 |          dfa_size (str, optional): DFA size for ripgrep. Defaults to "1G".
 |          multiline (bool, optional): Search in multiline mode. Defaults to False.
 |          multiline_dotall (bool, optional): Search in multiline dotall mode. Defaults to False.
 |          field_match_separator (str, optional): Field match separator. Defaults to "ÇÇÇÇÇ".
 |      
 |      Returns:
 |          pd.DataFrame: Dataframe containing the search results.
 |  
 |  find_all_in_variable(self, regular_expressions: Union[list, str], variable: Union[bytes, str], ignore_case: bool = True, binary: bool = True, dfa_size: str = '1G', multiline: bool = False, multiline_dotall: bool = False, outputencoding: str = 'utf-8', field_match_separator: str = 'ÇÇÇÇÇ') -> pandas.core.frame.DataFrame
 |      Searches for all regular expressions in the input variable.
 |      
 |      Args:
 |          regular_expressions (Union[list, str]): Regular expressions to be searched.
 |          variable (Union[bytes, str]): Input variable to be searched.
 |          ignore_case (bool, optional): Ignore case while searching. Defaults to True.
 |          binary (bool, optional): Search in binary mode. Defaults to True.
 |          dfa_size (str, optional): DFA size for ripgrep. Defaults to "1G".
 |          multiline (bool, optional): Search in multiline mode. Defaults to False.
 |          multiline_dotall (bool, optional): Search in multiline dotall mode. Defaults to False.
 |          outputencoding (str, optional): Output encoding. Defaults to "utf-8".
 |          field_match_separator (str, optional): Field match separator. Defaults to "ÇÇÇÇÇ".
 |      
 |      Returns:
 |          pd.DataFrame: Dataframe containing the search results.
 |  
 |  sub(self, df: pandas.core.frame.DataFrame, dryrun: bool = True) -> list
 |      Substitutes the matched regular expressions in the input files.
 |      
 |      Args:
 |          df (pd.DataFrame): Dataframe containing the search results.
 |          dryrun (bool, optional): If True, performs a dry run. Defaults to True.
 |      
 |      Returns:
 |          list: List of files where the substitutions were made.
 |  
 |  sub_in_variable(self, df: pandas.core.frame.DataFrame, variable: Union[bytes, str]) -> Union[bytes, str]
 |      Substitutes the matched regular expressions in the input variable.
 |      
 |      Args:
 |          df (pd.DataFrame): Dataframe containing the search/replace results.
 |          variable (Union[bytes, str]): Input variable to be changed.
 |      
 |      Returns:
 |          Union[bytes, str]: Substituted variable.
 |  
 |  ----------------------------------------------------------------------
 |  Static methods defined here:
 |  
 |  cb(variable: Union[str, int, bytes]) -> bytes
 |      Converts the input variable to bytes.
 |      
 |      Args:
 |          variable (Union[str, int, bytes]): Input variable to be converted.
 |      
 |      Returns:
 |          bytes: Converted variable in bytes.
 |  


```
