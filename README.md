# easy-location

```python
from geopy.geocoders import Nominatim
from tqdm import tqdm
from geopy.extra.rate_limiter import RateLimiter

geolocator = Nominatim(user_agent="cobanov")
geocode = RateLimiter(geolocator.geocode, min_delay_seconds=1)

tqdm.pandas()
df['gcode'] = df['full_adress'].progress_apply(geocode)
df['point'] = df['gcode'].apply(lambda loc: tuple(loc.point) if loc else None)
df[['latitude', 'longitude', 'altitude']] = pd.DataFrame(df['point'].tolist(), index=df.index)
```
