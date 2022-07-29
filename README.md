# Supabase: auth by specific domain

Stackoverflow question:
https://stackoverflow.com/questions/71591949/restrict-supabase-sign-up-to-a-specific-domain

1. SQL Function:

```
CREATE FUNCTION
  public.check_user_domain()
  RETURNS TRIGGER AS
  $$
  BEGIN
    IF NEW.email NOT LIKE '%@test.com' THEN
      raise exception 'INCORRECT_DOMAIN';
    END IF;

    RETURN NEW;
  END;
  $$ LANGUAGE plpgsql SECURITY DEFINER;
```

2. Trigger:

```
CREATE TRIGGER
  check_user_domain_trigger
  before INSERT ON auth.users
  FOR EACH ROW
  EXECUTE PROCEDURE
    public.check_user_domain();
```

Youtube:

[![How to make it](https://img.youtube.com/vi/C-HoRO7Wrhg/0.jpg)](https://www.youtube.com/watch?v=C-HoRO7Wrhg)
