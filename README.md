# Zadanie rekrutacyjne - wykrywanie fake-newsów
#### _Opis zadania_

Wykrywanie "fake newsów" - klasyfikacja artykułów z tytułami. Celem zadania jest opracowanie klasyfikatora, który na podstawie treści i tytułu artykułu będzie przypisywał jedną z czterech klas (szczegóły w źródle).

Źródła i objaśnienia do danych:
http://www.fakenewschallenge.org/

#### Rozwiązanie problemu

W pliku ```bodies.csv``` znajdują się treści różnych artykułów wraz z przypisanymi do nich kluczami. W pliku ```stances.csv``` znajdują się przykładowe tytuły do nich wraz z etykietami. Aby zapewnić spójność danych, iterując po każdym rekordzie danych z nagłówkami, przyklejałem do nagłówka treść odpowiedniego artykułu.

Póżniej należało każdy taki rekord przetworzyć na listę tokenów. Zrobiłem to za pomocą narzędzi ```CountVectorizer``` oraz ```TfidfTransformer``` z biblioteki ```scikit-learn```.

Dane podzieliłem póżniej na uczące i walidacyjne w proporcjach odpowiednio 80:20.

Przetestowałem 2 rozwiązania, które wydawały mi się dosyć sensowne w podejściu do NLP. Pierwszym był **naiwny klasyfikator Bayesa**. Przy jego pomocy uzyskałem dokładność na poziomie ~ 75%. Drugim podejściem były **sieci neuronowe**. Testując różne konfiguracjie hiperparametrów, dobrym rozwiązaniem okazał się być perceptron 3-warstwowy z warstwami ukrytymi o liczbie neuronów odpowiednio 10 i 2. Tutak uzyskałem dokładność na poziomie ~ 92%. Do uczenia zastosowałem algorytm ADAM, który wności dużo usprawnień (minibache, inercję, normalizaję pochodnych).

#### Pobieranie i uruchamianie projektu
Należy sklonować projekt z githuba:
```sh
$ git clone https://github.com/nowaq99/fake-news.git
```

Pojawi się folder z całym projektem. Interesuje nas plik ```zadanie.ipynb```. Jest to plik notatnika Jupyter, więc trzeba zainstalować JupyterLab. Na przykład za pomocą komendy:
```sh
pip install jupyterlab
```
Póżniej należyw wykonać linijki kodu związane ze wczytywaniem danych, tworzeniem wektorów tokenów słów oraz uczeniem dowolną metodą. Aby uzyskać wynik z nowych danych, muszą one byc w formacie jakim został model uczony, czyli sklejony string nagłówka i treści artykułu, przekształcony na listę tokenów.
```sh
predicted = clf.predict(X_test)
```
