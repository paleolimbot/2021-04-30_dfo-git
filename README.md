
``` r
prof_meta <- read.csv("argo_profile_meta.csv")
prof <- read.csv("argo_profiles.csv")
countries <- ne_countries(returnclass = "sf")
```

``` r
ggplot(prof_meta) +
  annotation_spatial(countries) +
  shadow_spatial(
    st_bbox(
      c(xmin = -65, xmax = -35, ymin = 50, ymax = 62),
      crs = 4326
    ),
  ) +
  geom_spatial_point(aes(longitude, latitude), crs = 4326) +
  annotation_scale(location = "br") +
  coord_sf(crs = 3857) +
  theme_void()
```

![](README_files/figure-gfm/argo-prof-map-1.png)<!-- -->

``` r
ggplot(prof, aes(y = pres, x = temp)) +
  geom_line(
    aes(group = interaction(file, n_prof)),
    orientation = "y",
    alpha = 0.1
  ) +
  facet_wrap(vars(month(date, label = TRUE)), nrow = 3) +
  scale_y_reverse() +
  theme_bw() +
  theme(strip.background = element_blank())
```

![](README_files/figure-gfm/argo-temp-1.png)<!-- -->

``` r
ggplot(prof, aes(y = pres, x = psal)) +
  geom_line(
    aes(group = interaction(file, n_prof)),
    orientation = "y",
    alpha = 0.1
  ) +
  facet_wrap(vars(month(date, label = TRUE)), nrow = 3) +
  scale_y_reverse() +
  theme_bw() +
  theme(strip.background = element_blank())
```

![](README_files/figure-gfm/argo-psal-1.png)<!-- -->