# mlmmlm-icu-bcakup-1

this repo is a back up of site mlmmlm.icu

to fix page switching problem and generate index.html please run:

``` python
import os
import re

base_path = os.getcwd()


# run this script on /t/topic

def find_all_file(base):
    for root, ds, fs in os.walk(base):
        for f in fs:
            if f.endswith('.html'):
                fullname = os.path.join(root, f)
                yield fullname


def main():
    base = base_path
    with open("index.html", "wt", encoding='utf-8') as f:
        index_content = "<!DOCTYPE html>"
        for fullname in find_all_file(base):
            try:
                print(fullname)
                fin = open(fullname, "rt", encoding="utf-8")
                data = fin.read()
                data = data.replace('%3Fpage=', '_page=')  # fix "上一页" "下一页"

                title = re.search("<title>(.+?)</title>", data).group(1)
                index_content += "<a href='{}'>{}</a></br></br>".format("file:///" + fullname, title)
                fin.close()

                fin = open(fullname, "wt", encoding="utf-8")
                fin.write(data)
                fin.close()
            except Exception:
                print("Error :" + fullname)
        f.write(index_content)


if __name__ == '__main__':
    main()

```

This is a example file the script generated.
https://github.com/mlmmlm-icu/mlmmlm-icu-bcakup-1/blob/main/t/topic/index.html

