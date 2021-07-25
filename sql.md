
**1)**

link: https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=446618&extra=page%3D5%26filter%3Dsortid%26sortid%3D311%26sortid%3D311


Q1: Given the table about posts
date | user_id | post_id | content_type | extra

 - content_type: 'view', 'comment', 'photo', 'report'
 - extra: post text, comment text, report type = {'SPAM', ...}


Q: What is the total number of posts posted yesterday for each type of report?

**answer**

SELECT count(1)
FROM post
WHERE DATE = DATE() - INTERVAL('1 DAY')
GROUP BY report_type


Q2: When a post is reported by the user as spam, the reviewers will manually review and remove them. Given the table about review_removal

date | reviewer_id | post_id

What percentage of the posts viewed by the users yesterday is reported as spam?


