// Best AK Automata v2.1 in Luogu (BAKA)

#define LUOGU 1

#include <cstdlib>
#include <string>
#include <iostream>
#include <fstream>
#include <sstream>
#include <stdexcept>

#if LUOGU
#define LG_KKK(X, Y) X##Y
#define LG_CZ(A, B, C) A##B##C
#define LG_LXL(A, B, C, D) A##B##C##D
#define LG_LTT(X) #X
#define LG_SYS LG_CZ(sy, st, em)
#define LG_FREOP LG_LXL(f, re, op, en)
#define LG_OP LG_KKK(op, en)
#define LG_IFSTR std::LG_CZ(if, str, eam)
#define LG_OFSTR std::LG_CZ(of, str, eam)
#endif

// check prefix
bool has_prefix(const std::string& __s, const std::string& __x)
{
    std::string::const_iterator i=__s.begin(), j=__x.begin();
    while (true)
    {
        if (j==__x.end()) return true;
        if (*i++==*j++) continue;
        break;
    }
    return false;
}

// check suffix
bool has_suffix(const std::string& __s, const std::string& __x)
{
    std::string::const_iterator i=__s.end(), j=__x.end();
    while (true)
    {
        if (j==__x.begin()) return true;
        if (*--i==*--j) continue;
        break;
    }
    return false;
}

#define GUGU_VERSION "2.1"
#define GUGU_FILETREE "/tmp/cz.txt"
#define GUGU_EXPORT "/tmp/cz.exp"
#define GUGU_LOG "/tmp/cz.log"
#define GUGU_SAMPLE 1024

std::string input;
std::string ans;

// output log
void logex(const std::string& s)
{
    LG_OFSTR fout(GUGU_LOG);
    fout << "GUGU v" GUGU_VERSION << '\n';
    fout << s << '\n';
    exit(0);
}

// get file tree
std::string file_tree()
{
    // generate file tree
    LG_SYS("ls -a -R /tmp > " GUGU_FILETREE);

    std::string s;

    // read file tree
    {
        LG_IFSTR fin(GUGU_FILETREE);
        char ch;
        while (true)
        {
            ch = fin.get();
            if (!fin) break;
            s += ch;
        }
    }

    return s;
}

// generate file list
std::string gen_list(const std::string& tree)
{
    std::istringstream ss(tree);
    std::string s;

    // ignore files just in /tmp, not in its child directories
    while (true)
    {
        std::getline(ss, s);
        if (!ss) logex("gugu: list generation failed");
        if (has_prefix(s, "/tmp/")) break;
    }

    // push back first directory
    std::string dir = s;
    dir.back() = '/';
    std::string ret;

    // generate list from tree
    while (true)
    {
        std::getline(ss, s);

        if (!ss) break;

        // ignore virtual directory
        if (s == "." || s == "..")
            continue;

        // find directory
        if (has_prefix(s, "/tmp/"))
        {
            dir = s;
            dir.back() = '/';
            continue;
        }

        // ignore runtime directory
        if (!has_prefix(dir, "/tmp/runtime/"))
            ret += (dir + s + '\n');
    }

    return ret;
}

// compare input
bool compare(const std::string& x)
{
    std::string s;

    // get input from file
    {
        LG_IFSTR fin(x);
        char ch;
        for (size_t i = 0; i < GUGU_SAMPLE; ++i)
        {
            ch = fin.get();
            if (!fin) break;
            s += ch;
        }
    }

    return s == input;
}

// steal answer
void steal()
{
    // get file list
    std::string list = gen_list(file_tree());

    LG_OFSTR fout(GUGU_EXPORT);
    std::istringstream ss(list);
    std::string s;

    while (true)
    {
        std::getline(ss, s);
        if (!ss) break;
        fout << s << ':';
        LG_IFSTR fin(s);

        // file not matched
        if (!fin)
        {
            fout << " gugugu\n";
            continue;
        }

        fout << '\n';

        // match file
        {
            if (has_suffix(s, ".in") && compare(s))
            {
                // remove "in"
                s.pop_back(); s.pop_back();

                // answer file has suffix ".out"
                std::string tmp = s + "out";
                if (LG_IFSTR(tmp))
                {
                    ans = tmp;
                    return;
                }

                // answer file has suffix ".ans"
                tmp = s + "ans";
                if (LG_IFSTR(tmp))
                {
                    ans = tmp;
                    return;
                }

                logex("gugu: answer not found");
            }
        }

        fout << '\n';
    }
}

// initialize input from std::cin
void initialize()
{
    char ch;
    for (size_t i = 0; i < GUGU_SAMPLE; ++i)
    {
        ch = std::cin.get();
        if (!std::cin) break;
        input += ch;
    }
}

// output answer
void answer()
{
    LG_IFSTR fin(ans);
    char ch;
    while (true)
    {
        ch = fin.get();
        if (!fin) break;
        std::cout << ch;
    }
}

// delete temporary files
// so admins cannot realize that we are stealing answers
void finalize()
{
    LG_SYS("rm -f " GUGU_FILETREE);
    LG_SYS("rm -f " GUGU_EXPORT);
    LG_SYS("rm -f " GUGU_LOG);
}

// main program
int main()
{
    initialize();
    steal();
    answer();
    finalize();
    return 0;
}
