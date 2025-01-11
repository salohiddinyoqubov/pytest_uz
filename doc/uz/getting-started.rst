.. _get-started:

Boshlash
===================================

.. _`getstarted`:
.. _`installation`:

``pytest``ni o'rnatish
----------------------------------------

``pytest`` pytest uchun Python 3.8 yoki undan yuqori versiya yoki PyPy3 talab qilinadi.

1. Buyruqlar qatorida quyidagi buyruqni bajaring:

.. code-block:: bash

    pip install -U pytest

2. To'g'ri versiyani o'rnatganingizni tekshiring:

.. code-block:: bash

    $ pytest --version
    pytest 8.3.3

.. _`simpletest`:

Birinchi testingizni yarating
----------------------------------------------------------

Funktsiya va testni o'z ichiga olgan ``test_sample.py`` nomli yangi fayl yarating:

.. code-block:: python

    # content of test_sample.py
    def func(x):
        return x + 1


    def test_answer():
        assert func(3) == 5

Test

.. code-block:: pytest

    $ pytest
    =========================== test session starts ============================
    platform linux -- Python 3.x.y, pytest-8.x.y, pluggy-1.x.y
    rootdir: /home/sweet/project
    collected 1 item

    test_sample.py F                                                     [100%]

    ================================= FAILURES =================================
    _______________________________ test_answer ________________________________

        def test_answer():
    >       assert func(3) == 5
    E       assert 4 == 5
    E        +  where 4 = func(3)

    test_sample.py:6: AssertionError
    ========================= short test summary info ==========================
    FAILED test_sample.py::test_answer - assert 4 == 5
    ============================ 1 failed in 0.12s =============================

``[100%]`` barcha test holatlarini bajarishning umumiy jarayonini bildiradi. Tugatgandan so'ng, pytest muvaffaqiyatsizlikka uchraganini ko'rsatmoqda. Chunki ``func(3)`` ``5`` qaytarmaydi.

.. note::

    Siz ``assert``ni  test natijalarini tekshirish uchun ishlatishingiz mumkin. pytest’ning :ref:`Advanced assertion introspection <python:assert>` xususiyati assert ifodasining oraliq qiymatlarini aqlli tarzda ko'rsatadi, bu esa sizga JUnit eski metodlarining ko'plab nomlaridan qochishga yordam beradi :ref:`<testcase-objects>`.


Bir nechta testlarni o'tkazing
----------------------------------------------------------

``pytest`` joriy katalogdagi va uning ichki kataloglaridagi test_*.py yoki \*_test.py shaklidagi barcha fayllarni ishga tushiradi. Umuman olganda, u :ref:`standart test topish qoidalari <test discovery>`ga amal qiladi.



Ma'lum bir xatoning tashlab ketilganligini ya'ni ``raise``ni tekshiring
--------------------------------------------------------------

Ba'zi bir kodning xatolarini tashlab ketishni tekshirish uchun :ref:`raises <assertraises>` yordamchisidan foydalaning:

.. code-block:: python

    # content of test_sysexit.py
    import pytest


    def f():
        raise SystemExit(1)


    def test_mytest():
        with pytest.raises(SystemExit):
            f()

Siz shuningdek, :ref:`raises <assertraises>` tomonidan taqdim etilgan kontekstdan foydalanib, kutilgan xatoning tashlab ketilgan :class:`ExceptionGroup`ning bir qismi ekanligini tekshirishingiz mumkin:


.. code-block:: python

    # content of test_exceptiongroup.py
    import pytest


    def f():
        raise ExceptionGroup(
            "Group message",
            [
                RuntimeError(),
            ],
        )


    def test_exception_in_group():
        with pytest.raises(ExceptionGroup) as excinfo:
            f()
        assert excinfo.group_contains(RuntimeError)
        assert not excinfo.group_contains(TypeError)

Test funksiyasini “quiet” hisobot rejimi bilan bajarish:


.. code-block:: pytest

    $ pytest -q test_sysexit.py
    .                                                                    [100%]
    1 passed in 0.12s

.. note::

    ``-q/--quiet`` flagi ushbu va undan keyingi misollarda chiqishni qisqa tutadi.

Bir nechta testlarni bir klassga guruhlash
--------------------------------------------------------------

.. regendoc:wipe

Bir nechta testni ishlab chiqqaningizdan so'ng, ularni bir klassga guruhlashni xohlashingiz mumkin. pytest bir nechta testni o'z ichiga olgan klass yaratishni osonlashtiradi:

.. code-block:: python

    # content of test_class.py
    class TestClass:
        def test_one(self):
            x = "this"
            assert "h" in x

        def test_two(self):
            x = "hello"
            assert hasattr(x, "check")

``pytest`` barcha testlarni :ref:`Python testlarni topish qoidalari <test discovery>`ga rioya qilib aniqlaydi, shuning uchun u ``test_`` bilan boshlanadigan funksiyalarni ham topadi. Subklass yaratishning hojati yo'q, ammo klassni ``Test`` bilan boshlashni unutmang, aks holda klass o‘tkazib yuboriladi. Modulni faqat uning fayl nomini berib ishga tushirishimiz mumkin:

.. code-block:: pytest

    $ pytest -q test_class.py
    .F                                                                   [100%]
    ================================= FAILURES =================================
    ____________________________ TestClass.test_two ____________________________

    self = <test_class.TestClass object at 0xdeadbeef0001>

        def test_two(self):
            x = "hello"
    >       assert hasattr(x, "check")
    E       AssertionError: assert False
    E        +  where False = hasattr('hello', 'check')

    test_class.py:8: AssertionError
    ========================= short test summary info ==========================
    FAILED test_class.py::TestClass::test_two - AssertionError: assert False
    1 failed, 1 passed in 0.12s

Birinchi test o‘tdi va ikkinchisi muvaffaqiyatsiz bo‘ldi. Siz osongina tekshiruvda oraliq qiymatlarni ko‘rishingiz mumkin, bu esa muvaffaqiyatsizlik sababini tushunishga yordam beradi.

Testlarni klasslarda guruhlash quyidagi sabablarga ko‘ra foydali bo‘lishi mumkin:

* Testlarni tashkil etish
* Faqat shu klassda bo‘lgan testlar uchun fixturelarni baham ko‘rish
* Klass darajasida belgilangan markalarni qo‘llash va ularni barcha testlarga avtomatik tarzda tatbiq etish

Testlarni klasslar ichida guruhlayotganda e'tibor berish kerak bo‘lgan narsa shundaki, har bir testda klassning noyob instansi mavjud bo‘ladi. Agar har bir test bir xil klass instansiyasini
bo‘lishsa, bu test izolyatsiyasiga jiddiy zarar yetkazadi va yomon test amaliyotlarini targ‘ib qiladi.
Buni quyida ko‘rishingiz mumkin:


.. regendoc:wipe

.. code-block:: python

    # content of test_class_demo.py
    class TestClassDemoInstance:
        value = 0

        def test_one(self):
            self.value = 1
            assert self.value == 1

        def test_two(self):
            assert self.value == 1


.. code-block:: pytest

    $ pytest -k TestClassDemoInstance -q
    .F                                                                   [100%]
    ================================= FAILURES =================================
    ______________________ TestClassDemoInstance.test_two ______________________

    self = <test_class_demo.TestClassDemoInstance object at 0xdeadbeef0002>

        def test_two(self):
    >       assert self.value == 1
    E       assert 0 == 1
    E        +  where 0 = <test_class_demo.TestClassDemoInstance object at 0xdeadbeef0002>.value

    test_class_demo.py:9: AssertionError
    ========================= short test summary info ==========================
    FAILED test_class_demo.py::TestClassDemoInstance::test_two - assert 0 == 1
    1 failed, 1 passed in 0.12s

E'tibor bering, klass darajasida qo‘shilgan atributlar *klass atributlari* bo‘lib, ular barcha testlar tomonidan umumiy foydalaniladi.

Funktsional testlar uchun noyob vaqtincha direktoriyani so‘rash

--------------------------------------------------------------

``pytest`` o'zida :std:doc:`Ichki fixturelar/funksiyalar argumentlari <builtin>`ni taqdim etadi, bu orqali tasodifiy resurslar, masalan, noyob vaqtinchalik direktoriyani so‘rashingiz mumkin:

.. code-block:: python

    # content of test_tmp_path.py
    def test_needsfiles(tmp_path):
        print(tmp_path)
        assert 0

Test funktsiyasining imzosi (signature) o'rniga ``tmp_path`` nomini kiritganingizda, ``pytest`` bu resursni yaratish uchun fixture-fabrikasini avtomatik tarzda chaqiradi. Test ishga tushishidan oldin, ``pytest`` har bir test uchun alohida vaqtinchalik direktoriyani yaratadi:


.. code-block:: pytest

    $ pytest -q test_tmp_path.py
    F                                                                    [100%]
    ================================= FAILURES =================================
    _____________________________ test_needsfiles ______________________________

    tmp_path = PosixPath('PYTEST_TMPDIR/test_needsfiles0')

        def test_needsfiles(tmp_path):
            print(tmp_path)
    >       assert 0
    E       assert 0

    test_tmp_path.py:3: AssertionError
    --------------------------- Captured stdout call ---------------------------
    PYTEST_TMPDIR/test_needsfiles0
    ========================= short test summary info ==========================
    FAILED test_tmp_path.py::test_needsfiles - assert 0
    1 failed in 0.12s

Vaqtinchalik direktoriyalarni va fayllarni boshqarish haqida ko'proq ma'lumotni :ref:`Temporary directories and files <tmp_path handling>` bo'limidan olishingiz mumkin.

Qanday turdagi o'rnatilgan :ref:`pytest fixture'lar <fixtures>` mavjudligini quyidagi buyruq orqali bilib olishingiz mumkin:

.. code-block:: bash

    pytest --fixtures   # shows builtin and custom fixtures

Shuni unutmangki, bu buyruq ``_`` bilan boshlanadigan fixture'larni ko'rsatmaydi, faqat ``-v`` opsiyasi qo'shilganida ular ko'rsatiladi.

O'qishni davom ettiring
-------------------------------------

Testlaringizni o'z ish jarayoningizga moslashtirish uchun quyidagi qo'shimcha pytest resurslarini ko'rib chiqing:

* :ref:`usage` - buyruq satri orqali pytest'ni qanday ishga tushirishni ko'rsatuvchi misollar
* :ref:`existingtestsuite` - mavjud test to'plamlari bilan ishlash usullari
* :ref:`mark` - ``pytest.mark`` mexanizmi va uni qanday ishlatish haqida ma'lumot
* :ref:`fixtures` - testlaringiz uchun zarur bo'lgan resurslarni ishlab chiqish
* :ref:`plugins` - pytest uchun plagin ishlab chiqish bo'yicha qo'llanma
* :ref:`goodpractices` - testlar uchun virtualenv va tuzilma bo'yicha yaxshi amaliyotlar


