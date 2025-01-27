.. _get-started:

Boshlash
===================================

.. _`getstarted`:
.. _`installation`:

``pytest``ni o'rnatish
----------------------------------------

``pytest`` quyidagilarni talab qiladi: Python 3.8+ yoki PyPy3.

1. Buyruqlar qatorida quyidagi buyruqni bajaring:

.. code-block:: bash

    pip install -U pytest

2. To'g'ri versiyani o'rnatganingizni tekshiring:

.. code-block:: bash

    $ pytest --version
    pytest 8.3.3

.. _`simpletest`:

Birinchi testni yarating
----------------------------------------------------------

``test_sample.py`` nomli yangi fayl yarating, u funksiya va testni o'z ichiga olsin:

.. code-block:: python

    # test_sample.py mazmuni
    def func(x):
        return x + 1


    def test_answer():
        assert func(3) == 5

Testni ishga tushiring:

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

``[100%]`` barcha test holatlarini ishga tushirish jarayonidagi umumiy progressni bildiradi. Test yakunlangandan so'ng, pytest ``func(3)`` ``5`` qiymatini qaytarmagani uchun muvaffaqiyatsizlik hisobotini ko'rsatadi.

.. note::

    Test natijalarini tasdiqlash uchun ``assert`` bayonotidan foydalanishingiz mumkin. pytest'ning :ref:`Ilg'or tasdiq introspektsiyasi <python:assert>` xususiyati ifodalardagi qiymatlarni aqlli tarzda hisobot qiladi, bu esa :ref:`JUnit usullarining ko'plab nomlaridan <testcase-objects>` foydalanishni talab qilmasligiga yordam beradi.

Bir nechta testlarni ishga tushirish
----------------------------------------------------------

``pytest`` joriy katalogdagi va uning ostidagi kataloglardagi ``test_*.py`` yoki ``*_test.py`` shaklidagi barcha fayllarni ishga tushiradi. Umuman olganda, u :ref:`standart testlarni aniqlash qoidalariga <test discovery>` amal qiladi.

Ma'lum bir xatolik qayd etilganini tasdiqlash
--------------------------------------------------------------

Xatolik qayd etilishini tasdiqlash uchun :ref:`raises <assertraises>` yordamchisidan foydalaning:

.. code-block:: python

    # test_sysexit.py mazmuni
    import pytest


    def f():
        raise SystemExit(1)


    def test_mytest():
        with pytest.raises(SystemExit):
            f()

:ref:`raises <assertraises>` tomonidan taqdim etilgan kontekstdan foydalanib, :class:`ExceptionGroup` tarkibida kutgan xatolik borligini tasdiqlash mumkin:

.. code-block:: python

    # test_exceptiongroup.py mazmuni
    import pytest


    def f():
        raise ExceptionGroup(
            "Guruh xabari",
            [
                RuntimeError(),
            ],
        )


    def test_exception_in_group():
        with pytest.raises(ExceptionGroup) as excinfo:
            f()
        assert excinfo.group_contains(RuntimeError)
        assert not excinfo.group_contains(TypeError)

Test funksiyasini "quiet" rejimida ishga tushiring:

.. code-block:: pytest

    $ pytest -q test_sysexit.py
    .                                                                    [100%]
    1 passed in 0.12s

.. note::

    ``-q/--quiet`` flagi natijalarni qisqa ko'rsatish uchun ishlatiladi.

Testlarni classlarda guruhlash
--------------------------------------------------------------

.. regendoc:wipe

Bir nechta testlarni classda guruhlash uchun:

.. code-block:: python

    # test_class.py mazmuni
    class TestClass:
        def test_one(self):
            x = "bu"
            assert "b" in x

        def test_two(self):
            x = "salom"
            assert hasattr(x, "check")

``pytest`` barcha ``test_`` bilan boshlanuvchi funksiyalarni aniqlaydi. Classni ``Test`` bilan boshlashni unutmang, aks holda class o'tkazib yuboriladi. Testni ishga tushiring:

.. code-block:: pytest

    $ pytest -q test_class.py
    .F                                                                   [100%]
    ================================= FAILURES =================================
    ____________________________ TestClass.test_two ____________________________

    self = <test_class.TestClass object at 0xdeadbeef0001>

        def test_two(self):
            x = "salom"
    >       assert hasattr(x, "check")
    E       AssertionError: assert False
    E        +  where False = hasattr('salom', 'check')

    test_class.py:8: AssertionError
    ========================= short test summary info ==========================
    FAILED test_class.py::TestClass::test_two - AssertionError: assert False
    1 failed, 1 passed in 0.12s

Testlarni classlarda guruhlash quyidagi foydalarga ega:

* Testlarni tashkil qilish
* Faqat class darajasidagi fixturelardan foydalanish
* Belgilarni class darajasida qo'llash

Har bir test uchun alohida class instansiyasi yaratiladi. Bu test izolyatsiyasini ta'minlaydi:

.. code-block:: python

    # test_class_demo.py mazmuni
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

Vaqtincha direktoriyalar bilan ishlash
--------------------------------------------------------------

``tmp_path`` fixture'idan foydalanish:

.. code-block:: python

    # test_tmp_path.py mazmuni
    def test_needsfiles(tmp_path):
        print(tmp_path)
        assert 0

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

Fixture'larni ko'rish:

.. code-block:: bash

    pytest --fixtures

Davom etish uchun
-------------------------------------

Qo'shimcha manbalar:

* :ref:`usage` - buyruq satri misollari
* :ref:`existingtestsuite` - mavjud testlar bilan ishlash
* :ref:`mark` - belgilash mexanizmlari
* :ref:`fixtures` - resurslarni boshqarish
* :ref:`plugins` - plaginlar bilan ishlash
* :ref:`goodpractices` - yaxshi amaliyotlar
