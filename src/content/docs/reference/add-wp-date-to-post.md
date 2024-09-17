
---
title: WordPress rss date time
---

```
<lastBuildDate><?php echo mysql2date(' r', $post->post_date, false); ?></lastBuildDate>
```

another example:

```
<pubDate><?php echo mysql2date( 'D, d M Y H:i:s +0300', get_post_time( 'Y-m-d H:i:s', true ), false ); ?></pubDate>
```
