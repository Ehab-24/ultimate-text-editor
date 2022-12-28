# Ultimate Text Editor

Ultimate Text Editor is a console based text editor written entirely in C++ with no GUI.

## Description

This was one of my very first OOP projects, and one of my hardest yet. It is a console based text editing software where you can edit multiples documents simultaneously, save and open plain text files and put passwords on them which will automatically encrypt all data for the outsiders. Although there is no GUI involved, I still tried my best to add aesthetics using special ASCII symbols and console colors. The software provides several different functionalities of common text editors such as, find and replace, words and lines count, opening multiple files, file encryption, a mini word game, common shorcuts for faster editing and much more.

## Classes

The core of the program are the following three classes:

* Line 
    * a custom implementation of the String class.
* Document 
    * holds an array of Line.
* Text Editor/Master class
    * holds an array of documents and manages the programs flow.

### Line Class

Line is a custom implementation of the famous String class. It merely holds a char pointer and the length of the character array it points to. In addition, it holds all the functionality related to a single line in a document, e.g; searching for a subString, words count, encryption and decryption, find and replace functionality etc. Following is the header file for Line class.

> **private:**

    static bool isLower(char);
    static bool isUpper(char);
    static bool isChar(char);

    void construct(int);

    Line getStr(int, int)const;

    bool matchFound(char)const;

    bool alreadyExists(Line* strs, int)const;

    bool strFound_CaseInSen(const Line&, int)const;
    bool strFound_CaseSen(const Line&, int)const;
    bool strFound(const Line&, int, bool)const;

    void expandArr(int*&, int&, int)const;
    void expandArr(Line*&, int&)const;

    void replaceOneWord_expand(const Line&, int, int);
    void replaceOneWord_contract(const Line&, int, int);
    void replaceOneWord_simple(const Line&, int);

    int prevWordIndex(int)const;	//expects 'dci'.
    int nextWordIndex(int)const;

    unsigned int totalLength()const;

  > **public:**
 
    void highlight(const Line&, int*, int)const;

    int len;
    char* Cs;

    friend class Document;
    friend class TextEditor;

    int findPrevSpace(int)const;
    int findNextSpace(int)const;


    Line();
    Line(int);
    Line(const Line&);
    Line(const char*);
    ~Line();

    void print(int = 0, int = 0, bool = true)const;
    static void print(char);

    void encrypt(ofstream&)const;
    void decode(ifstream&);

    void save(ofstream&)const;
    void load(ifstream&);

    void insert_at(int, char);
    void remove_at(int);

    int find_next(const Line&, int, bool)const;
    int find_prev(const Line&, int, bool)const;

    int* findNextAll(const Line&, int, int&, bool)const;
    int* findPrevAll(const Line&, int, int&, bool)const;

    int* find_all(const Line&, int&, bool)const;

    void toUpper(int);
    void toLower(int);

    Line line_cat(const Line&)const;

    int findReplaceNext(const Line&, const Line&, int, bool);
    int findReplacePrev(const Line&, const Line&, int, bool);

    int* findReplaceAll(const Line&, const Line&, int&, bool);

    int* addPrefix(const Line&, const Line&, int&, bool);
    int* addPostfix(const Line&, const Line&, int&, bool);

    void removeSubstring(int, int);

    unsigned int wordcount()const;

    unsigned int longestWordlen()const;
    unsigned int shortestWordlen()const;

    Line word_game(const Line&, int&)const;

    bool operator==(const Line&)const;
  
### Document Class

Similarly we have a document class that builds on the line class to implement functionalities of a document, such as, highlighting text, cursor position, line duplication, line deletion etc. Following is the header file for Document class.

> ""private:**

	  void deleteIndexes();
  
    void removeLine();

	  void ask_password()const;

> **public:**

    friend class Line;

    Line* Ls;
    int nol, lastLineNo, docLines;
    int dri, dci;
    bool vert_mov,
      highlighted,
      encoded;
    string name, password;

    highlightedText HT;

    Document();
    Document(int);

    void printStats()const;

    static void outline();

    void fill_HT(const Line&, bool, int*&);

    void highlight();
    void unhighlight();

    void displaycount(const char* msg, float count, int ri)const;

    void word_count()const;

    void longest_word()const;

    void shortest_word()const;

    void avg_length()const;

    void doc_lines()const;

    void doc_name()const;

    void saveEncoded(ofstream&)const;

    void save(ofstream&)const;
    int load(ifstream&);

    void printLs(int, int, bool = true)const;

    void print(int, bool = true, bool = true)const;

    void ENTER_AddNewLine();

    void Arrow_Keys(char, int&, int&);

    void insertChar(char);

    void Cursor(int, int)const;

    void Update_DocLines();

    void BACKSPACE_removeLine();
    void BACKSPACE_removeChar();
    void BACKSPACE_removeWord();

    void DELETE_removeLine();
    void DELETE_removeChar();
    void DELETE_removeWord();

    int FindAll(const Line&, bool, int*);

    void FindNextAll(const Line&, bool, int*);
    void FindPrevAll(const Line&, bool, int*);

    int FindReplaceNext(const Line&, const Line&, int&, bool);
    int FindReplacePrev(const Line&, const Line&, int&, bool);

    int FindReplaceNextAll(const Line&, const Line&, bool);
    int FindReplacePrevAll(const Line&, const Line&, bool);

    int FindReplaceAll(const Line&, const Line&, bool);

    int AddPrefix(const Line&, const Line&, bool);
    int AddPostfix(const Line&, const Line&, bool);

    int WordCount()const;

    float AvgWordLen()const;

    unsigned int longestWordLength()const;	//Also find longest word.
    unsigned int shortestWordLength()const;	//Also find shortest word.

    int Word_Game(const Line&compare, Line*&)const;
  
### HighlightedText Struct:
  
    struct highlightedText {
      int** indexes;
      Line tofind;
      bool caseFlag;
      int* clrs;
    };
    
### Text Editor Class

Finally, we have the **text editor** or **master** class which brings it all together to create a complete text editor. Following is the header file for this class:

> **private:**

    Document* Ds;
	    int cdi,
		  nod;

    void PrintShortcuts();

    char PrintStartScreen();

    void MergeDocuments(string, string);

    void SwitchToNext();

    void SwitchToPrev();

    void OpenNewDoc();

    void loadAndPrint(Document&);

    void save(Document&);

    void alt(Document&);

> **public:**

    TextEditor();

    void run();
    
Working on this project was truly a magnificent experience. It enabled me to see the life cycle of bigger software projects with a clearer vision and improved my work ethic and understanding ten folds.

## Authors

Ehab Sohail [Ehab T-48](ehabs1775@gmail.com)

## Acknowledgments

* [@SarfrazRazaOfficial](https://www.youtube.com/@SarfrazRazaOfficial)
* [ITU](https://itu.edu.pk/)
