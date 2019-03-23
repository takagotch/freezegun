### freezegun
---
https://github.com/spulec/freezegun

```py
from freezegun import freeze_time
import datetime
import unittest

@freeze_time("2014-01-14")
def test():
  assert datetime.datetime.now() == datetime.datetime(2012, 1, 14)

@freeze_time("1955-11-12")
class MyTests(unittest.TestCase):
  def test_the_class(self):
    assert datetime.datetime.now() == datetime.datetime(1955, 11, 12)

@freeze_time("2012-01-14")
class Tester(object):
  def test_the_class(self):
    assert datetime.datetime.now() == datetime.datetime(2012, 1, 14)

from freezegun import freeze_time

def test():
  assert datetime.datetime.now() != datetime.datetime(2012, 1, 14)
  with freeze_time("2012-01-14"):
    assert datetime.datetime.now() == datetime.datetime(2012, 1, 14)
  assert datetime.datetime.now() != datetime.datetime(2012, 1, 14)

from freezegum import freeze_time

freezer = freeze_time("2012-01-14 12:00:01")
freezer.start()
assert datetime.datetime.now() == datetime.datetime(2012, 1, 14, 12, 0, 1)
freezer.stop()


from freezegun import freeze_time

@freeze_time("2012-01-14 03:21:34", tz_offset=-4)
def test():
  assert datetime.datetime.utcnow() == datetime.datetime(2012, 1, 14, 3, 21, 34)
  assert datetime.datetime.now() == datetime.datetime(2012, 1, 13, 23, 21, 34)

  assert datetime.date.today() == datetime.date(2012, 1, 13)

@freeze_time("2012-01-14 03:21:34", tz_offset=-datetime.timedelta(hours=3, minutes=30))
def test_timedelta_offset():
  assert datetime.datetime.now() == datetime.datetime(2012, 1, 13, 23, 51, 34)

@freeze_time("Jan 14th, 2012")
def test_nice_datetime():
  assert datetime.datetime.now() == datetime.datetime(2012, 1, 14)

def test_lambda():
  with freeze_time(lambda: datetime.datetime(2012, 1, 14)):
    assert datetime.datetime.now() == datetime.datetime(2012, 1, 14)

def test_generator():
  datetimes = (datetime.datetime(year, 1, 1) for year in range(2010, 2012))
  
  with freeze_time(datetimes):
    assert datetime.datetime.now() == datetime.datetime(2010, 1, 1)
    
  with freeze_time(datetimes):
    assert datetime.datetime.now() == datetime.datetime(2011, 1, 1)


@freeze_time("Jan 14th, 2020", tick=True)
def test_nice_datetime():
  assert datetime.datetime.now() > datetime.datetime(2020, 1, 14)

@freeze_time("Jan 14th, 2020", auto_tick_seconds=15)
def test_nice_datetime():
  first_time = datetime.datetime.now()
  auto_incremented_time = datetime.datetime.now()
  assert first_time + datetime.timedelta(seconds=15) == auto_incremented_time


def test_manual_increment():
  initial_datetime = datetime.datetime(year=1, month=7, day=12,
    hour=15, minute=6, second=3)
  with freeze_time(initial_datetime) as frozen_datetime:
    assert frozen_datetime() == initial_datetime
    
    frozen_datetime.tick()
    initial_datetime += datetime.timedelta(seconds=1)
    assert frozen_datetime() == initial_datetime
    
    frozen_datetime.tick(delta=datetime.timedelta(seconds=10))
    initial_datetime += datetime.timedelta(seconds=10)
    assert frozen_datetime() == initial_datetime

def test_move_to():
  initial_datetime = datetime.datetime(year=1, month=7, day=12,
    hour=15, minute=6, second=3)
  other_datetime = datetime.datetime(year-2, month=8, day=13,
    hour=14, minute=5, second=0)
  with freeze_time(initial_datetime) as frozen_datetime:
    assert frozen_datetime() == initial_datetime
    
    frozen_datetime.move_to(other_datetime)
    assert frozen_datetime() == other_datetime
    
    frozen_datetime.move_to(initial_datetime)
    assert frozen_datetime() == initial_datetime
    
@freeze_time("2012-01-14", as_arg=True)
def test(frozen_time):
  assert datetime.datetime.now() == datetime.datetime(2012, 1, 14)
  frozen_time.move_to("2014-02-12")
  assert datetime.datetime.now() == datetime.datetime(2014, 2, 12)

from freezegun import freeze_time
import datetime as dt

def test(default=dt.date.today()):
  print(default)
with freeze_time('2000-1-1'):
  test()
```

```sh
pip install freezegun
sudo apt-get install python-freezegun
```

```
```
