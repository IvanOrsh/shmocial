## API Routes (starting point)

| page                     | route (endpoint)                                                                  | description                                     |
| ------------------------ | --------------------------------------------------------------------------------- | ----------------------------------------------- |
| `/`                      | -                                                                                 | home page                                       |
| `/signin`                | `POST  /api/login`                                                                | login page (?)                                  |
| `/sigup`                 | `POST /api/signup`                                                                | signup page                                     |
| search feature           | `GET /api/search?q=user`                                                          | -                                               |
| current user profile     | `GET /api/profile`                                                                | -                                               |
| `/feed`                  | `/api/posts/feed?page=1`                                                          | -                                               |
| `/profile`               | `POST /api/posts`, `GET /api/posts?page=1`                                        | create post/tweet, load more posts/tweets       |
| `/profile/edit-post/:id` | `PATCH /api/posts/:id`, `DELETE /api/posts/:id`                                   | edit post/tweet, delete post/tweet              |
| `/following`             | `GET /api/users/:id/following?page=0`                                             | following page                                  |
| `/followers`             | `GET /api/users/:id/followers?page=0`                                             | followers page                                  |
| `/account`               | `POST /api/users/avatar`, `GET /api/signout`                                      | account page to upload avatar, sign out (more?) |
| `/[username]`            | `GET /api/follows?user_id=3`, `POST /api/follows/`, `DELETE /api/follows/user_id` | page to follow / unfollow                       |

## DB Schema (starting point)

users table:

1. id bigserial (auto increment field) primary key
2. username citext (case insensitive text) (ex: foobar, FooBar should be the same!)
3. password text
4. avatar text
5. is_admin boolean (for simple role based authorization)
6. created_at timestamp default now()
7. updated_at timestamp default now()

---

posts (tweets?) table:

1. id bigserial (auto increment field) primary key
2. user_id bigint **references** users(id)
3. content text
4. created_at timestamp default now()
5. updated_at timestamp default now()

---

follows:

1. user_id bigint **references** users(id)
2. follower_id bigint **references** users(id)
3. created_at timestamp default now()
4. updated_at timestamp default now()

unique(user_id, follower_id) - constraint - user a can only follow user b one time!
