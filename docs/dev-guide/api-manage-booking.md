# Document API Manage Booking

---

## 1. Tìm kiếm booking

!!! info "GET: /bookingsrv/api/bookings/search"
    Tìm kiếm booking

### Headers
???+ example "Headers"

    - Authorization (string, required)

        !!! quote ""

            Token để xác thực người dùng

            VD: `Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiI1ZjhkMThjOThiNDgxMTFkZDQ3MTJhYmZfdGNkbEBnb3RhZGkuY29tIiwiYXV0aCI6IlJPTEVfQjJDLFJPTEVfUEFSVE5FUiIsIlgtaWJlLWQiOiIzMjU3MTM1MTcwM2U3MTc4ZmJmNTFjYzI4YzhkYTBkZDU5YTA5YWY3NTQ0NTU0YmMwMzk2YjY1ODVjNTExMjkzYmFjYTAzY2FlNmEyZTUzNGI1ODY3ODhiZWYyZjhiMjllNDQ1OTQyM2Y2MzAyMzE5M2M4NDg2NzkyMGE3M2YzNmM1YjIzOTljNzIxZWI5ZmMwZjJiMWJkZTAwZmViZjE3YWNhNjc2M2JjZjNhZDRkNWNhMTkxMmUzNWQ3MmZkZTIxMjUxMDhhZDlmNzFjZTU4ODNkN2YzN2JiNTM3NDFiNjhmYTk3NWEwZTk1YjhhZDI1MGNjM2YyZDdjNmViY2QxMmE0OTQ5MjJhMjY1MzU2NDI5YmMxN2EwYWU5ZWJiYzU2MzI5YzQ0NDk4ZDQ1YmFkOTMxZGY4ODFiOTM5MmUwOWI1ZmRmOWMzMThlY2NlZDc3MjFmMDY3NGQxNDZhZTZmMzI1YjNhMDBmM2E0YmE4YTMyNzJjMWQ1MDNhODNlZmU5YTVkOGYwNjcyMTM2ZWU3N2Q1ZTAzNDg3ZjBmMjExMWQ2YWIyMTdmMjNhZDY0MmZmNDQ0MTMzMjc3YmRhMGE3MDQzOTk3NWExMTM1ZWRmMDRmNjJiNDY3YjE3MDMyZGEyNmQzZjMyYzk3NmQzOTA0ZDI4NDUxZWVhYzBkNDcyYWU3N2RmOWFiNTFkNDhiY2EwZDEyNjA2NTRjMWQ2NzhiMmYwZjYxYWFiMGQwNWQwZjdmNmY3NTI1NDcyMDczZDQ3MjA2NWFkOWJkYmQ5NjljNjYzMDE4YTVlOTBjNzkyZTkxY2Q0ZjgyZmFiNjk3MTJmYTkyMzEyMDY1YTI1OTUzYTJhNDMzYzY3OWYzYzc1ZTI2MWUzMDI3NjAxYmYxZDUzY2NkNjUxZmY1MDBmYjYwNTgwNDg3YzIzYjRlZGI0YWJlMTI3OGQ5MTEwYjUwNzA4ODQ2MjEwMWRjZTdkYzEyODg4ZTZkZDJjZWQxNWQ4ZDczOGMwOGVhNzA1MjBlMTM1NGM4YzRkMTkwNTVhYWMzNzg4Y2QwMGEwZDdkMzQxODRkMGJmOWI4OTU1MTU0ZDg1MzBmYWU5NWFjOTM2ZmVlMzYwYjM3OGU0OTcyYjYzYWY2MGVjYzBkY2RlODY1NzFiZjRlYTE4MTkwNTRmYjkzNjU1NTlmY2NmOWYyZjRmNmJiZjkxY2ZlODhiOTI3ODMwYjU4ODZkMTBlYjUxZDAwYjkwY2JjMjFiYzdkYThkNGY2NjY0YzlhYTgxMjRlMDBmYjI4MTcyZTVkYzJlODY1YzUwZGRkMjdhMDVjZTJhMjg1NmViNjY5OWM5NWI1NmE2NzZjZDg1N2JjYWU4MjU0YTNhOTgzZGI5YTRhYTllYzM3NDE4NGEwNGY3ZmUwMDg0ZTQ0OTRiOGY3NGQ3Y2I2MWJjNzIwZWI1MDM5NTE2NzdlNmNlMjNkN2YzYTcxOGZhMTFmYzEzNTBmZTFmZTU3ZWFhNzFjMGIxNGU1OTNjZGEzYzJkNGFiMWMzZjc3MzU4MzY1NjQzYmVmN2MxNmI5Njc4ZDc5Y2NhZjU0ODgxODYyNmUyYjRhMWVkMjhlZjQ1NGNjNzllZThkNDlmOWY0ZmMxNzI0YzhkNmI4ZWE4MTc3N2E3M2NiNGE4OGEzNDhjMGNlYmNmZTNkOGQxYzBkZTQzN2NkYmI0ZTVhNGQ0Nzk3YWNmZmNjMzgxZjRlMzJmNTZkMzUzMmI5YTk3NjZiZDIxMWEzNjU5YzUwMGY0YzY5YTNkMTUyOTBlNzA2YTUzM2FhOGNkMzRhNTM5NDdmNzAxOWViZjUxMTIwNTRmMGQxZTk3MWI0NmJmMmM3YTJlM2YzYThlNjhmZmNjNjkwNmJkOTE1NGZjM2UxNTQ0MzZkMTJkNWFmMDU5MTZkMjg5ODEyMTVhMWUyMWE1Yjg4NjUxNGZjM2JhMjUyNTYwMzIzNTA4ODYzNzkzYTgyNTg1YjI5ODBhMDYxYjg4MzM1ZTlhYmZlMzYwYTgwNjI5YjhjMjY5M2MwMDRiMTllNWM3ODFlNDU4MDJlNTFhZjI3OTFjOTEzZTM4YWZiYTgyOTcwZmYzMjRjYjhkZDZiMmE1NDE4MzQyNGU1Y2QzNThiYmI5MDY1NmU3Y2VmYjhlNDBiZTM4MzAxZjM0ZDVmMmE0ZDdkZTIyODIzMjVlYmRlMDQzNTU3MzVkZTAzODA0Y2NlYjAxZjI1ZGEzZWVjYzI4ZjdhOTFkYjljNTZhZDVjYjdiN2RiZjEzYjI0ZGNkY2U4YTJkNjI3MzVmZTY3MjI2MDBjYjJiZmEwODM2NTc5ODFmMWI5MDdhZDllNjljMmVmNDQ0ZDBiNmY0NDA4ZTQ0ZDllNzYzZmRmZTBhZDQxNjFhOGJjYmJjNDI1MjBhZTYxNzFmMzYyZGZlNzY1OWEyYTJiMzBmYzY5ZjFlMDFiNjAyYzRkZGUyY2ZhOTJlNWZmY2UwNTU0NzlmOTdjMjk3OGM4MTI5YmM4MWZjOGJmMzJiYmI5OTY4YTc0NjM5ODE3YTE5YzFkMGJkYTYwMDY2Zjg4OTY4MjljN2M3YzdhMjE5NTM4YWQyZTMwMjcwNTIwOTUyOWQwNjNkMzFiYzNhYjJjMDVjOWYxYTk3OTg2YzkwOWNlZjNlOTgxMWMxNzY1ODRlMjcwM2YxMTdlMmI3ZjY5ZTQ3MjY0ZGQ0YTA3NjJmYzI2YTQ2NzUzYWM0OGE3YTdiNzhlOTM3ZDBjMjMxMWNiZTFhYzljMTNiZTE5OGI4NmJhNzU3MzY4ZDZhOWZkNjAxMWQ5NjRjYTMyNGQ1NjM1MzA3N2JlYWNjOTg0MTVmNzIzNmNjMjA3OTRiNDhlMjQwMmQ0ZjJiMDI4MDk5ODM1Y2E5YWM4MjE4MmY5YzVhYWVkZWVjZWRiMTlmOTM1NzMxZmE4Y2M5MzFhYzBhZmZhMTQzMTBhN2E1OTBmNDlmMmYwZTZiMTgyODljMGJjMzI5YjAzNGQxOGU5N2U1NDlmNzM4YjY4MzhmOTk0YzI4ZmIwY2UyMjJmYzY3OGFjY2IyYzAwMmE3MzJmYTY5MmFiOWUxYjRjZDE5NzdmMDgxMzY3Y2I0NWQ5MTliODAyMjU3NDliZGM0OWQ1NDFkMjkwNDllNTU5MGFiMzlmYTE4ZTlkMjZlNDM5MWEyNGE5ZmRhNmM2OWI0ZmM3ZDUzM2VhNTQzNTJlMzVjOTQyMGJiZGYwMDg0NjY5MWIyYmY0ZmI0ZDA1ZTA3MGIxYjU2MjMzYjg5NDJkMDg4NWU3YjJjYzkzOTc4YmZiYTE4ZDM1NDlmZGJiNWUxNzdlNDY0NjY1NWViMWI4OWM4NDFlOWU3MTFjOTdkYjI1MTE4ZWUyNThkZTg4YjNlNTAzYjFmMWQ3Y2EyY2Q0YzY3MzRmOGJiY2Q5ZmY2NDc0YzM4MDljNjg4NzJhMjg0MjMwN2EzZmFlMjE0N2RmOThjMmJlOTliZDE0ZmE5N2I3Y2EyMzhmYjE5NjVlNzI2ZGI4MDdhMzJkNGVjOGU1ZjI1OGQ0Zjg5ZjhjYjY3N2ZjZWQ4OGRhZTA5OTM5MjdmOGM1YThmZjEzOWI4ZGViNTMwMTk0ODM5MWJlM2E2OWI0YjI3NmI5OWQ1N2U1NjU2YjY1MjYxMDM3NmQxZTBhZjBlNTRjNTg3OGE0ZGJhMjE5OWNjYzU4M2E1MDRkNDdlNzI2OTAyMTQxMzRjYWUyZDg2N2U3ZTRkYTFmNzgzMzg5OTA4NDhhZDE3YzU0MDEyOWFkNjViN2Y3NTY5YWRhMmMyMDNlMWMzZTIwNGExOWY3OTc1ZWI1NGQxNmNlMTRkMDMxNTI3ZjkwYmZjNTdiNWNhYzUxYmUxNjA2NGVmODNkYWEwNDgwNjllOThkMjM5NGFkZWNlMjAwNmVkZTEwMzkwZmFhNDcwZmViM2Y5NTc0ZjA3MTVkYmJhN2ZjNzY2NGUyYTdmZTBjMjJmYWNkOTRiMDFiYWYyYzEyNTEwMmFiNmY5YTEwM2QzNzRmZmFkYTUzYWJhZmE2Zjc5NTcwZGZmMTNhYjBiOTE1ZmIwZjFmYjBlMWJjMjY5N2I0ZjUxNjczMjdiMzc1OGQzNGRmYzI3ZDZlZGIwZWU5OTFhYjJmMmUyNGJkYWUxZWNlMTgxMTMwMjgwNjliNTNhMDM5MDcyNzg3YmRkNDdmNjVhNTQ3MDc3NjVhMmI5NDJiNjJlYWQ2MTgwMGQxNTQ3M2FjZmFmYmE2MTZjZWQwOWFlZmE5ZjZkODY5MGZkNDgyMWY5OGIzYjM3YjJlZTE5MjY1NTZlMWZjMGYyNjE2NDllNzMyNWYwNDFkZTNhOTkwYmE1N2ZiZjFjZWJkYjE3ZWNkZmFhZDUxYjk2ZGE4YzllOTcwNzQyYmM4YTFkZjJhMzk3ZmQwMzQyMDhkOTJhZWVjNGIzNWRlZjVmMzEzMGU1ZTU1MzNjZGJlMDk2YzgwZDY0YzA1ZDYyNjQ4YzJmYjRlMjgzZjNhM2VmNjg4YjAyMjFlNDY4OGZkYTg3Yzc5YWI0YzVjZTc5Y2RiYzgxODNmMzE4Y2E3MGQyZDJkOGY5ODQ2MmU2MmMwYTQ5NjE5Zjc4MGU0OTI1ZjYwZGRkZjVhZDNlNDkxZmMzZTM4YTk5MTMzMmY4ODBlYjA0N2E1ODJkNDc1MjgxMDAyMzUxZTE1OTAzNDRiM2VhMzJiNjQ3NjFiMjQ3OWU0NGRmYTUyNjUxNzMzZDNiYmNjOTYwOTQ2ZDQyNGM4ZjkxMmQ1OWVlMzEzMTUwODQ4OGY2ODY2MWQ4YTM2ZmNjZDllOGIxNjAzNjg1NzNkNmFlMGE0NWZhOWQwNzczNGI3ZjllNmRiYzRhYjJhZGEyYWQ1YmJmOGFjNDMwNDc3YjcwZTE2MDAxNmZiNmQ1NGRjZTc2NTQ1NDExNDIxODc4OTlkNThhMDk0YzE1M2I4ZGVkMGIzNjhjYTBmYjg5NjdlZjJiZDlhZjIyMTJhODI2MGI4ZDRiYzBhYzBjYjliZjAyMTExYjZhNjQyNDg3MzlmZWU3Y2EyMzUxYzRkZmYwMjc0N2FkNzhlZTg5NTMxODZlMTZiNTJlZDQxNDI3NjJjN2Y4NzZmMmRlMzk1ZjI2OGViYjM2ZjM0NTI3NjgyMzA5OWYwYmFlYjhkNDYwOTE2MWUyODNkYmMxZWNjNTU0NmU3ZTJlYjMyZjUxOTUzNDFhMjE0ZmYwZDMzNmE4Mjc5ZWI1NDZiMmZmNGM3YjY0MWZiNWU4ZGFhMjZkMmFhYzEyYTc2YzI1M2I4Y2JmZWU0MmRlY2Q3NWM5ZDYyYjI2ZTVkNTY1ZDRhNWQwNDQ5YjA5NTA2OTkxNWU5M2U5N2JhOWQ4N2VmZTVjMzRjNWY3NjhmMTM0YmVjMjBlOTY0MjE5YmUxMDg4MGE2NDA2Y2RhM2FkMDRmM2IyMjRhMmJmMDY2YjI3NWY0MWI5YTM0OGI1MjAzZWUyYjM4Y2EzOGZiMjk0ZGQzZTZkZDJiYzIxN2E0NTA3YzllMzhkMzZkYzcwM2I1YjlkNzE3ZGM3NDM4MGRmNzYzY2E2ZGRkOWIxODliMGIyODY4ZDgyYmMyMmQwMGNlYjc4ODE1Mzg4ZTFlMjE2ZmVjZDUzMDIyMTU0MWVhY2Y1NmI1ZjJlMzU5ODMyZjY4YzBiMGE3Mzg2YTJhZDY4YWM1YTE3NGJjM2ZlZTcxMzk4OGM1YTdlOTkyODYyNDAwNTdmOThiOTg1ZmY4NmRjN2NkOTM5MjgyYjM4YjNkOGZkZDQyYTRlNmYxZDI4NGIyNDE2MjQxNGVjMTEwMTU4YjM2NmNiYmY3NmE2NTZhZjNkODc3ODVjNmY1MTk5ZDM4ZjA0NTA5MGQxZmU1NDliNmRiMmQ0NmMzNDE5NWI0ZWQ4OTg3NTMyOTljNmM5MjRkMDdlMGIwNDY1ODI0YTE5NjBiNWVhNTc1ODM4NDg5MDkzMDI4NmM3Y2M5NzE3YjUyMGE4YzQxZDY4ZTc2NzQ4OTMwMjI1MjYxMTNjNWI3Y2E4Njg2M2E3ODgwMmExOGQzODIxMjc3YTU1YzAwN2M5MTE1ZjFjM2RmYWNkZDhiYmI5YzczYmFkYWMyMTkwZGZlMmMyZTViNGJmM2JhOWFhZWJlODhiYTg0ZDlkMmI5MWU3YzRmYzk4OWYzMmVlOWU4OTViOTM5ZWY0NTRkZjEyMmFmZWMyYjg0YmQ5OGU3YzdmZWVkNjdhMTE0OTM3MzljZmE2MjY4MDNjNjFlMWUwNWI5OTNhNTE3ODNhN2IwYjA5YTQ4ZWRjMzg0Yjg5ZTE1NzMwZTE4ZjdmZmYyNDIyOTdiMWI3MWQxYzk4MzI2ZGRmOTllNzQwMjVjMmQwMGIzNWVkMDQzZDg4MTgyNWMyZjgxMmE4NTg0YTM5MTkzN2UxMWRiZDQwOTJlMDBmMDAxOGRjMzFhOTkxM2Y0M2Q0MTU5MTEzYmQ4ZTliZTZhNzJkZTE5MTE1YjAzNmI4ODZmODUxYTYwNTlhY2E4NWU5NGMxMjFkODQyMzA1ZjkyOTljMWQxYjk1MjJmZDJmODE1ZDE0MTc3YTg4NWNkMDJjZDc4OGFlYWJlYjViMmIwZmQwYTZkZGJmZWNiYWRiYjI1NDQzYjk4MDllZWFmMzc3MmVkYTNmN2I2MDQ0MTA2OGE4ZmVhMTM1OWRmNWI2YWIzYTcxNjcyZTAwNDQxMWYxMzA4ZDMwODFmNzAzMTE2MThlNTU1YTUxZWIxYjY5Y2ViNmQzNzFjMDY1YjhmNDEyNWM1NmIyYTA5NjRmOGExOGU4NmM0ZWFmYzA1OThkYWNjZmI1N2YyMDAzMGE1ZjFiNmVhNGFmZjE5MGY4ZTIxZDg2Mjg1ODA4Y2FkOTI1NmE1YTY0ZmEwYjEwMzk4MjY1ZDM3NDUyMGFhMTM5MDQwZThlMTVlZjUxNjZhNDQ2NTJhMDQzZTU5MThmMWE4M2NhODY4MDg0OTQzY2ZjNWFmYTk4ZTg0OTc0NjljNjVmYjM3MjlhMTgzY2I1MGIyYzc3NDYwZjJjNGViNjY0YmIyM2NjMzZlZmYyOGY5MjNjNGQ0MzA0OGIxMTViZDA3ODllYmNiZTFlNDEzMGNmNWFiZTRhNzM0NTQyZDU3ZDE0ZjUzM2RlNjFhYTI2MDBiODgzMTA1Yzk4MjBjNGI4ZGVlOGMwNTJjNDU0NTdmMDU4ZGY3Y2Q4MTc0ZmNiOGI4NTZlMWZhOWZkNWRjMzU0NjE2NDQ3ZWY5ZjFkN2Y5YjlmMjQ0NzA2MzdiNzM3YTJiOGE4ZThhYjk5YzEwZWU5OTc2ZGMzYmQ1NTZhOTBiMmQzYTNjMGU3OWJlOGFhYWQ4MTIxODU3N2VjNzM5NDBhYWY2YzA3NmI4OGQzNWY4MjNjNzYyYTZiZGJkZDJkOGI2MWViMjAzODE3MmY5NmQyZmI4YzQzZTEyMGE0NjU0MmMwODVlOTNjYzMyMTlhNmRhOTdmMjVkOWU5YjBjZjc1NWFhNDFiOWVjNzk2NTFiYTcyYTkzNTg1MzlhNDlmMmRhYjU5MTA1NDdmN2NhMGQ2ZDc0YWE4YjhkNzg2OGYwOWRkNmE0ZDQ1NTZkODc2NDI0ODA0Yzg2ZWMyMWFhMDM0ODVhZmY1YzQ2ZjRiMWY2YmU4Nzk4YTk3NTBmMGRhZGE1MzkwMzI0ZTE3N2RmM2Y1M2NhMzg5YTlkZWQ3MTVkNzlmNzRmNzIyOTU2NjcwZTAwOGFhZTMwMjUzN2E5YWY0ODZlZTgzZDM1ZmQ3NWZkYzQ5ZDcwMzI1OGUzYzNmZWFlNjU1YzMzYmMzZjIwN2EzNWM5NzQzYjlmYTA5NjlmNGUxNDVjMDNjZmNlNWE0Mzk3ZGMyNmJiYWE2N2E0NTNlY2M4MGNhY2IzNjFkYWQwMWVhNzAzMDdiNzNjMWQ4OWEwNTg4ZjFlZjU1MWIzODc1NzQ1MTUzYTFhZmM3YTU0ZDgzMzk4ZGZjODY4NGE2ZjM5MzY1ZTZlM2Q3ZjYwMzdmODEyNDAxYTMyMjFlN2VhMzc1NzdjNzJiMGU0YmI0MmUxYmY1MWFmNjFhZDZjNDFjOWI2YmVkMTk1MTE5ODFkNjhmYThkNzI4MTFkNzJmYjAwOTkyZWVmMWRkNDE3ODRmN2VmMTYxZjczNTU4YTA4MWJjNGU4YjVmYmRlNjZiMzY4YjY3YzNiNDczNjc5ZTQ5NWY2YWZjNzdiY2NiYmQ5NTViNzFjMGNiMzJkODlmNDg4NWQ2N2U2NDZiZGFhNTM0ZTA1YjZjY2I5ZDI3ZDE2MGE5ODc2NTc1MjhiYzZkMzU3MDVlZGU2NDkxYWM1OTZlYjllMTgwOTJjYThkNThjMWFmN2Q2ZTA3NzRlMzUwNmZiNGI3MmJlNTI5OTkzZmJkNzU1YWRhMGZiNWY5ZGFhMWY5MTgzYWYxMzM4YmE3ODM5NjM4MWNiYjNmNmYxYWU5ZTA5YjY2OGM0NThiMDk1MmE1MDE5NDQ5OGE2NzcyYzIzMDZmYjM5MDU1OTE0ZGYwMTNlNmRkNGMwMmEyNzIyNTI0NzEzYmZiYjZmMzM0NjYzOTFmOTc5YTA3YzVhNzY2MDk2MmRmMTIyMWNhZTQxZDNmYjEwOGY0NzRmNDA1NDU2NmMwMDU4YzhlMDA4ZjNjZjcwMjQxMmY5ZjZjYThlN2RiZjllZjY4MTgxMTZiYzdjYTIzMWRiZDE2ODAzN2ViZDZiNDgwYzI4MDllYTkwY2I5YzMzYmM3NDA3YWJhZWU1YTk4NjQ0M2MxNzc4ZDEyMjZjODU1MGUwYmU5YzE4MmIyYjNkZjU5ZTgxNzE5MDI0M2ZmZWJhZTU0NzIxNjg2YTBiMzI4NDAzMDI1ZTk4NmJlM2ZlYWZlYmE2YzhhNDQxNmNhNDgxMzVmODQ1OTlmNmQxOThlYWI1MmFhMjdiZWMzNmU4YWYyMTMzOWRiMWNmZjY4ZDY4ZDg4MzM2OGY1MTcyYzY3OTRhMzFiMmE5ODdiNDYxMWMyOTEwZmY1OTVlOGQ2NTIzYzQxZTg1OWZjMGRjMzI3NWNlNmVlNjUyMjNkNTkyOTQ5ODcxZTI3NTA3MjhkZWM0NjcwZGEyZWEwZWQ5YTY2ZDM3MmQxNmE2MzdhZjU4NmM2MjBkNjNlZjkyZGQyMGY1N2UzMmM2Zjg0NWZmNGMzZTRkZTU5ZjM0ODVmYWM2NzlmYzZkY2VjMzJkMzRhNTg2ZjlhNGE3MWRhYzc2ZWQ4MDUxNTFhZDQ2OTY1YzljNDUyY2FlMmI1ZWEzMTQ0NjllOTAwYWZmOGJjZmFlODc4MGQ3OTUwNDBlYTNhMzAyZTBjYzgzOTAxZjU3OGJlODlkYzdiYjE2M2Y4NGYxOGU0M2JmMjY0ZGI3MjUzNDY3M2RhZTAyMTljYjNkYTY1NGRlODI4MTRhMjQzZWYxYTI4ZjQ5ZDhhMzU2OGE3Njg4OWYwZDc2NzdkNGYxY2Y0YjcyMThlYjA5MTQ4MGQyYTRiYzNlZDFhY2EwYTBjYmZhNjdjNWJjYWNmMTgyNjM0ODM5ZDFkOGZmYTViNzgwYjBhNjc4MTdlNDM3MzhmMzlmNWM0MThmZTdmYTc1NTQ2ODg4NWVjZjY5YThlOGUyOGQzMDk3OTUzNjZjNWFiNGYzZGJhYmFhMmZlNTI5YjQ1MzJiMjZiMGY5MWFhNzdkZjBkM2E2NmYwMTM1ZmU5ODNhMGE5YmZlOWUwMTdjNWJkZTg0ZTFhYTMyYTkiLCJYLWliZS1rIjoiZGE1NDA1MWNmZjI0ZWFjMCIsImV4cCI6MTY0NTI0NDU3Nn0.44O8keCfnY_3qQVLZ9Np5FQFUZsVO9rj1GQ9eQIP95XGfb4nUS5RktE6uBOsxmt8BB1-sKnJEtVEv9lAIaW7AQ`

### Parameters 
???+ example "Parameters"

    - bookingCode `query` (string, optional),

        !!! quote ""

            Mã tham chiếu đến booking

    - supplierType `query` (string, required),

        !!! quote ""

            Loại nhà cung cấp `AIR`, `HOTEL`, ...

    - listBookingStatus `query` (string[], optional),

        !!! quote ""

            Trạng thái booking. Các trạng thái booking: `PENDING`, `BOOKED`, `TICKET_ON_PROCESS`, `CONFIRMED`, `FAILED`, `EXPIRED`

    - fromLocationName `query` (string, optional),

        !!! quote ""

            Điểm đi

    - toLocationName `query` (string, optional),

        !!! quote ""

            Điểm đến

    - fromDate `query` (string, optional),

        !!! quote ""

            Tìm các booking có bookingDate lớn hơn hoặc bằng fromDate. Format `yyyy-MM-dd`

    - toDate `query` (string, optional),

        !!! quote ""

            Tìm các booking có bookingDate nhỏ hơn hoặc bằng toDate. Format `yyyy-MM-dd`

### Response 
#### Code 200
> OK

=== "Model"
    ???+ example "Model"
        - result (Array[BookingDTO], optional),
        - duration (integer, optional),
        - errors (Array[Error], optional),
        - infos (Array[Info], optional),
        - success (boolean, optional),
        - textMessage (string, optional)
        - page (Array[pageDTO], optional)

#### Code 400
> Bad Request

#### Code 401
> Unauthorized

#### Code 403
> Forbidden

#### Code 404
> Not Found

#### Code 500
> Unknown Internal Error

#### Code 503
> Service Unavailable

---

## 2. API Truy vấn kết quả xuất commit booking

!!! info "POST: /api/partner/query-trans"
    Truy vấn kết quả xuất commit booking

    !!! note "Chú ý"
        Yêu cầu bảo mật: Mã hóa dữ liệu và kèm theo chữ ký điện tử


### Request Body 

=== "Model"
    ???+ example "Model"                 

        - key (string, required),

            !!! quote ""

                Key giải mã dữ liệu (đã được mã hóa). Cách giải mã tham khảo mục: [Mã hóa dữ liệu truyền và xác thực chữ ký điện tử](/dev-guide/#3-ma-hoa-du-lieu-truyen-va-xac-thuc-chu-ky-ien-tu)

        - data (string, required),

            !!! quote ""

                Dữ liệu kèm theo chữ ký điện tử (đã được mã hóa). Cách giải mã tham khảo mục: [Mã hóa dữ liệu truyền và xác thực chữ ký điện tử](/dev-guide/#3-ma-hoa-du-lieu-truyen-va-xac-thuc-chu-ky-ien-tu)

                *Signature data schema:*

                ``` 
                <access_code>|<booking_number>
                ```    

                *Original data schema:*
                ```
                <access_code>|<booking_number>|<signature>
                ```

                - access_code (String, required)

                    !!! quote ""

                        Access code do Gotadi cung cấp cho Đối tác.

                - booking_number (String, required)

                    !!! quote ""

                        Mã dùng tham chiếu đến booking

=== "Example"
    ```json
    {
        "data": "string",
        "key": "string"
    }
    ```

### Response 
#### Code 200
> OK

=== "Model"
    ???+ example "Model"
        - key (String, required)

            !!! quote ""

                Key giải mã dữ liệu (đã được mã hóa). Cách giải mã tham khảo mục: [Mã hóa dữ liệu truyền và xác thực chữ ký điện tử](/dev-guide/#3-ma-hoa-du-lieu-truyen-va-xac-thuc-chu-ky-ien-tu)

        - data (String, required)

            !!! quote ""

                Dữ liệu kèm theo chữ ký điện tử (đã được mã hóa). Cách giải mã tham khảo mục: [Mã hóa dữ liệu truyền và xác thực chữ ký điện tử](/dev-guide/#3-ma-hoa-du-lieu-truyen-va-xac-thuc-chu-ky-ien-tu)

                *Signature data schema:*

                ``` 
                <access_code>|<booking_number>|<error_code>|<product_type>|<properties>|<return_url>|<total_amount>
                ```    

                *Original data schema:*
                ```
                <access_code>|<booking_number>|<error_code>|<product_type>|<properties>|<return_url>|<signature>|<total_amount>
                ```

                - access_code (String, required)

                    !!! quote ""

                        Access code do Gotadi cung cấp cho Đối tác.

                - booking_number (String, required)

                    !!! quote ""

                        Mã dùng tham chiếu đến booking

                - error_code (String, required)

                    !!! quote ""

                        [Mã lỗi](/dev-guide/#7-ma-loi)

                - product_type (String, optional)

                    !!! quote ""

                        Loại sản phẩm, có giá trị là `AIR` hoặc `HOTEL` tương ứng với loại sản phẩm được mua

                - properties (String, optional)

                    !!! quote ""

                        Các thông tin mở rộng trả về cho đối tác. `Json string`

                - return_url (String, optional)

                    !!! quote ""

                        Trang hiển thị kết quả giao dịch của Gotadi. Sử dụng trong trường hợp đối tác không tự xây dựng trang hiển thị kết quả cuối cùng.

                - total_amount (Double, required)

                    !!! quote ""

                        Tổng số tiền phải thanh toán.

#### Code 400
> Bad Request

#### Code 401
> Unauthorized

#### Code 403
> Forbidden

#### Code 404
> Not Found

#### Code 500
> Unknown Internal Error

#### Code 503
> Service Unavailable