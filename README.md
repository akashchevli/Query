# Query

SELECT COUNT(p.id), u.username
FROM tbl_users u ,tbl_posts p
WHERE u.id = p.user_id



SELECT u.username, m.image, COUNT(l.media_id)
FROM tbl_users u 
JOIN tbl_posts p 
ON u.id = p.user_id
JOIN tbl_media m
ON m.post_id = p.id
JOIN tbl_likes l
ON m.id = l.media_id
GROUP BY l.media_id


SELECT u.username, m.image, COUNT(l.media_id) AS "total_likes", c.media_id AS "total_comments"
FROM tbl_users u 
JOIN tbl_posts p 
ON u.id = p.user_id
JOIN tbl_media m
ON m.post_id = p.id
JOIN tbl_comments c
ON m.id = c.media_id
JOIN tbl_likes l
ON m.id = l.media_id
GROUP BY l.media_id
HAVING COUNT(c.media_id)



SELECT COUNT(following_id), u.username, (SELECT u.username from tbl_users u WHERE u.id = f.following_id) AS "following_name"
FROM tbl_users u
join tbl_followers_followings f
ON u.id = f.user_id
GROUP BY f.following_id
