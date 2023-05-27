swagger: '2.0'
info:
  version: 1.0.0
  title: PS3838 - Lines API Reference
  description: |
    All about odds and fixtures
  
    # Authentication 
    
    API uses HTTP Basic access authentication.You need to send Authorization HTTP Request header:  
    
    `Authorization: Basic <Base64 value of UTF-8 encoded "username:password">`
    
    Example:
    
    `Authorization: Basic U03MyOT23YbzMDc6d3c3O1DQ1`
  x-logo:
    url: ''
host: api.ps3838.com
schemes:
  - https
security:
  - basicAuth: []
paths:
  /v1/fixtures:
    get:
      tags:
        - Fixtures
      summary: Get Fixtures - v1
      description: Returns all **non-settled** events for the given sport. Please note that it is possible that the event is in Get Fixtures response but not in Get Odds. This happens when the odds are not currently available for wagering. Please note that it is possible to receive the same exact response when using **since** parameter. This is rare and can be caused by internal updates of event properties.
      operationId: Fixtures_V1_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: sportId
          in: query
          description: The sport id to retrieve the fixtures for.
          required: true
          type: integer
          format: int32
        - name: leagueIds
          in: query
          description: The leagueIds array may contain a list of comma separated league ids.
          required: false
          type: array
          items:
            type: integer
            format: int32
          collectionFormat: multi
        - name: isLive
          in: query
          description: To retrieve ONLY live events set the value to 1 (isLive=1). Missing or any other value will result in retrieval of events regardless of their Live status.
          required: false
          type: boolean
        - name: since
          in: query
          description: This is used to receive incremental updates. Use the value of last from previous fixtures response. When since parameter is not provided, the fixtures are delayed up to 1 minute to encourage the use of the parameter.
          required: false
          type: integer
          format: int64
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/FixturesResponseV1'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
      deprecated: true
  /v3/fixtures:
    get:
      tags:
        - Fixtures
      summary: Get Fixtures - v3
      description: Returns all **non-settled** events for the given sport. Please note that it is possible that the event is in Get Fixtures response but not in Get Odds. This happens when the odds are not currently available for wagering. Please note that it is possible to receive the same exact response when using **since** parameter. This is rare and can be caused by internal updates of event properties.
      operationId: Fixtures_V3_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: sportId
          in: query
          description: The sport id to retrieve the fixutres for.
          required: true
          type: integer
          format: int32
        - name: leagueIds
          in: query
          description: The leagueIds array may contain a list of comma separated league ids.
          required: false
          type: array
          items:
            type: integer
            format: int32
          collectionFormat: multi
        - name: isLive
          in: query
          description: To retrieve ONLY live events set the value to 1 (isLive=1). Missing or any other value will result in retrieval of events regardless of their Live status.
          required: false
          type: boolean
        - name: since
          in: query
          description: This is used to receive incremental updates. Use the value of last from previous fixtures response. When since parameter is not provided, the fixtures are delayed up to 1 minute to encourage the use of the parameter.
          required: false
          type: integer
          format: int64
        - name: eventIds
          in: query
          description: Comma separated list of event ids to filter by
          required: false
          type: array
          items:
            type: integer
            format: int32
          collectionFormat: multi
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/FixturesResponseV3'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
  /v1/fixtures/special:
    get:
      tags:
        - Fixtures
      summary: Get Special Fixtures - v1
      description: Returns all **non-settled** specials for the given sport.
      operationId: Fixtures_Special_V1_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: sportId
          in: query
          description: Id of a sport for which to retrieve the specials.
          required: true
          type: integer
          format: int32
        - name: leagueIds
          in: query
          description: The leagueIds array may contain a list of comma separated league ids.
          required: false
          type: array
          items:
            type: integer
            format: int32
          collectionFormat: multi
        - name: since
          in: query
          description: This is used to receive incremental updates. Use the value of last field from the previous response. When since parameter is not provided, the fixtures are delayed up to 1 min to encourage the use of the parameter.
          required: false
          type: integer
          format: int64
        - name: category
          in: query
          description: The category the special falls under.
          required: false
          type: string
        - name: eventId
          in: query
          description: Id of an event associated with a special.
          required: false
          type: integer
          format: int64
        - name: specialId
          in: query
          description: Id of the special.
          required: false
          type: integer
          format: int64
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/SpecialsFixturesResponse'
          examples:
            application/json:
              sportId: 4
              last: 636433059508250600
              leagues:
                - id: 487
                  specials:
                    - id: 1
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Will the 4th quarter be odd or even?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: 1/4 Totals
                      units: ""
                      status: I
                      event:
                        id: 1
                        periodNumber: 0
                      contestants:
                        - id: 1
                          name: Odd
                          rotNum: 100
                        - id: 2
                          name: Even
                          rotNum: 101
                    - id: 2
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Will the 3rd quarter be odd or even?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: 1/4 Totals
                      units: ""
                      status: I
                      event:
                        id: 1
                        periodNumber: 0
                      contestants:
                        - id: 3
                          name: Odd
                          rotNum: 100
                        - id: 4
                          name: Even
                          rotNum: 101
                    - id: 3
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Will the 2nd quarter be odd or even?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: 1/4 Totals
                      units: ""
                      status: H
                      event:
                        id: 1
                        periodNumber: 0
                      contestants:
                        - id: 5
                          name: Odd
                          rotNum: 100
                        - id: 6
                          name: Even
                          rotNum: 101
                    - id: 4
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Will the 1st quarter be odd or even?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: 1/4 Totals
                      units: ""
                      status: I
                      event:
                        id: 1
                        periodNumber: 0
                      contestants:
                        - id: 7
                          name: Odd
                          rotNum: 100
                        - id: 8
                          name: Even
                          rotNum: 101
                    - id: 5
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Will the 4th quarter be odd or even?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: 1/4 Totals
                      units: ""
                      status: null
                      event:
                        id: 2
                        periodNumber: 0
                      contestants:
                        - id: 9
                          name: Odd
                          rotNum: 100
                        - id: 10
                          name: Even
                          rotNum: 101
                    - id: 6
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Will the 3rd quarter be odd or even?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: 1/4 Totals
                      units: ""
                      status: I
                      event:
                        id: 2
                        periodNumber: 0
                      contestants:
                        - id: 11
                          name: Odd
                          rotNum: 100
                        - id: 12
                          name: Even
                          rotNum: 101
                    - id: 7
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Will the 2nd quarter be odd or even?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: 1/4 Totals
                      units: ""
                      status: I
                      event:
                        id: 2
                        periodNumber: 0
                      contestants:
                        - id: 13
                          name: Odd
                          rotNum: 100
                        - id: 14
                          name: Even
                          rotNum: 101
                    - id: 8
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Will the 1st quarter be odd or even?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: 1/4 Totals
                      units: ""
                      status: H
                      event:
                        id: 2
                        periodNumber: 0
                      contestants:
                        - id: 15
                          name: Odd
                          rotNum: 100
                        - id: 16
                          name: Even
                          rotNum: 101
                    - id: 9
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Who will win the NBA finals?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: Outright Winner
                      units: ""
                      status: I
                      contestants:
                        - id: 17
                          name: Golden State Warriors
                          rotNum: 100
                        - id: 18
                          name: Cleveland Cavaliers
                          rotNum: 101
                        - id: 19
                          name: San Antonio Spurs
                          rotNum: 102
                        - id: 20
                          name: Chicago Bulls
                          rotNum: 103
                - id: 578
                  specials:
                    - id: 10
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Who will win the WNBA finals?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: Outright Winner
                      units: ""
                      status: I
                      contestants:
                        - id: 21
                          name: Minnesota Lynx
                          rotNum: 100
                        - id: 22
                          name: Indiana Fever
                          rotNum: 101
                        - id: 23
                          name: Phoenix Mercury
                          rotNum: 102
                        - id: 24
                          name: Chicago Sky
                          rotNum: 103
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
      deprecated: true
  /v2/fixtures/special:
    get:
      tags:
        - Fixtures
      summary: Get Special Fixtures - v2
      description: Returns all **non-settled** specials for the given sport.
      operationId: Fixtures_Special_V2_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: sportId
          in: query
          description: Id of a sport for which to retrieve the specials.
          required: true
          type: integer
          format: int32
        - name: leagueIds
          in: query
          description: The leagueIds array may contain a list of comma separated league ids.
          required: false
          type: array
          items:
            type: integer
            format: int32
          collectionFormat: multi
        - name: since
          in: query
          description: This is used to receive incremental updates. Use the value of last field from the previous response. When since parameter is not provided, the fixtures are delayed up to 1 min to encourage the use of the parameter.
          required: false
          type: integer
          format: int64
        - name: category
          in: query
          description: The category the special falls under.
          required: false
          type: string
        - name: eventId
          in: query
          description: Id of an event associated with a special.
          required: false
          type: integer
          format: int64
        - name: specialId
          in: query
          description: Id of the special.
          required: false
          type: integer
          format: int64
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/SpecialsFixturesResponseV2'
          examples:
            application/json:
              sportId: 4
              last: 636433059508250600
              leagues:
                - id: 487
                  specials:
                    - id: 1
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Will the 4th quarter be odd or even?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: 1/4 Totals
                      units: ""
                      status: I
                      event:
                        id: 1
                        periodNumber: 0
                      contestants:
                        - id: 1
                          name: Odd
                          rotNum: 100
                        - id: 2
                          name: Even
                          rotNum: 101
                    - id: 2
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Will the 3rd quarter be odd or even?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: 1/4 Totals
                      units: ""
                      status: I
                      event:
                        id: 1
                        periodNumber: 0
                      contestants:
                        - id: 3
                          name: Odd
                          rotNum: 100
                        - id: 4
                          name: Even
                          rotNum: 101
                    - id: 3
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Will the 2nd quarter be odd or even?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: 1/4 Totals
                      units: ""
                      status: H
                      event:
                        id: 1
                        periodNumber: 0
                      contestants:
                        - id: 5
                          name: Odd
                          rotNum: 100
                        - id: 6
                          name: Even
                          rotNum: 101
                    - id: 4
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Will the 1st quarter be odd or even?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: 1/4 Totals
                      units: ""
                      status: I
                      event:
                        id: 1
                        periodNumber: 0
                      contestants:
                        - id: 7
                          name: Odd
                          rotNum: 100
                        - id: 8
                          name: Even
                          rotNum: 101
                    - id: 5
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Will the 4th quarter be odd or even?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: 1/4 Totals
                      units: ""
                      status: null
                      event:
                        id: 2
                        periodNumber: 0
                      contestants:
                        - id: 9
                          name: Odd
                          rotNum: 100
                        - id: 10
                          name: Even
                          rotNum: 101
                    - id: 6
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Will the 3rd quarter be odd or even?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: 1/4 Totals
                      units: ""
                      status: I
                      event:
                        id: 2
                        periodNumber: 0
                      contestants:
                        - id: 11
                          name: Odd
                          rotNum: 100
                        - id: 12
                          name: Even
                          rotNum: 101
                    - id: 7
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Will the 2nd quarter be odd or even?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: 1/4 Totals
                      units: ""
                      status: I
                      event:
                        id: 2
                        periodNumber: 0
                      contestants:
                        - id: 13
                          name: Odd
                          rotNum: 100
                        - id: 14
                          name: Even
                          rotNum: 101
                    - id: 8
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Will the 1st quarter be odd or even?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: 1/4 Totals
                      units: ""
                      status: H
                      event:
                        id: 2
                        periodNumber: 0
                      contestants:
                        - id: 15
                          name: Odd
                          rotNum: 100
                        - id: 16
                          name: Even
                          rotNum: 101
                    - id: 9
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Who will win the NBA finals?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: Outright Winner
                      units: ""
                      status: I
                      contestants:
                        - id: 17
                          name: Golden State Warriors
                          rotNum: 100
                        - id: 18
                          name: Cleveland Cavaliers
                          rotNum: 101
                        - id: 19
                          name: San Antonio Spurs
                          rotNum: 102
                        - id: 20
                          name: Chicago Bulls
                          rotNum: 103
                - id: 578
                  specials:
                    - id: 10
                      betType: MULTI_WAY_HEAD_TO_HEAD
                      name: Who will win the WNBA finals?
                      date: '2017-10-11T14:00:00Z'
                      cutoff: '2017-10-11T14:00:00Z'
                      category: Outright Winner
                      units: ""
                      status: I
                      contestants:
                        - id: 21
                          name: Minnesota Lynx
                          rotNum: 100
                        - id: 22
                          name: Indiana Fever
                          rotNum: 101
                        - id: 23
                          name: Phoenix Mercury
                          rotNum: 102
                        - id: 24
                          name: Chicago Sky
                          rotNum: 103
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
      deprecated: false
  /v1/fixtures/settled:
    get:
      tags:
        - Fixtures
      summary: Get Settled Fixtures - v1
      description: Returns fixtures settled in the last 24 hours for the given sport.
      operationId: Fixtures_Settled_V1_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: sportId
          in: query
          description: Id of the sport for which to retrieve the settled.
          required: true
          type: integer
          format: int32
        - name: leagueIds
          in: query
          description: The leagueIds array may contain a list of comma separated league ids.
          required: false
          type: array
          items:
            type: integer
            format: int32
          collectionFormat: multi
        - name: since
          in: query
          description: This is used to receive incremental updates. Use the value of last from previous response.
          required: false
          type: integer
          format: int64
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/SettledFixturesSportV1'
          examples:
            application/json:
              sportId: 0
              last: 0
              leagues:
                - id: 0
                  events:
                    - id: 0
                      periods:
                        - number: 0
                          status: 0
                          settlementId: 0
                          settledAt: '2017-09-03T18:21:22.3846289-07:00'
                          team1Score: 0
                          team2Score: 0
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
      deprecated: true
  /v3/fixtures/settled:
    get:
      tags:
        - Fixtures
      summary: Get Settled Fixtures - v3
      description: Returns fixtures settled in the last 24 hours for the given sport.
      operationId: Fixtures_Settled_V3_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: sportId
          in: query
          required: true
          description: Id of the sport for which to retrieve the settled.
          type: integer
          format: int32
        - name: leagueIds
          in: query
          required: false
          description: The leagueIds array may contain a list of comma separated league ids.
          type: array
          items:
            type: integer
            format: int32
          collectionFormat: multi
        - name: since
          in: query
          required: false
          description: This is used to receive incremental updates. Use the value of last from previous response.
          type: integer
          format: int64
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/SettledFixturesSportV3'
          examples:
            application/json:
              sportId: 0
              last: 0
              leagues:
                - id: 0
                  events:
                    - id: 0
                      periods:
                        - number: 0
                          status: 0
                          settlementId: 0
                          settledAt: '2017-09-03T18:21:22.3846289-07:00'
                          team1Score: 0
                          team2Score: 0
                          cancellationReason:
                            code: string
                            details:
                              correctTeam1Id: string
                              correctTeam2Id: string
                              correctListedPitcher1: string
                              correctListedPitcher2: string
                              correctSpread: '0.0'
                              correctTotalPoints: '0.0'
                              correctTeam1TotalPoints: '0.0'
                              correctTeam2TotalPoints: '0.0'
                              correctTeam1Score: '0'
                              correctTeam2Score: '0'
                              correctTeam1TennisSetsScore: '0'
                              correctTeam2TennisSetsScore: '0'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
  /v1/fixtures/special/settled:
    get:
      tags:
        - Fixtures
      summary: Get Settled Special Fixtures - v1
      description: Returns all specials which are settled in the last 24 hours for the given Sport.
      operationId: Fixtures_Specials_Settled_V1_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: sportId
          in: query
          description: Id of the sport for which to retrieve the settled specials.
          required: true
          type: integer
          format: int32
        - name: leagueIds
          in: query
          description: Array of leagueIds. This is optional parameter.
          required: false
          type: array
          items:
            type: integer
            format: int32
          collectionFormat: multi
        - name: since
          in: query
          description: This is used to receive incremental updates. Use the value of last from previous response.
          required: false
          type: integer
          format: int64
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/SettledSpecialsResponseV1'
          examples:
            application/json:
              sportId: 0
              last: 0
              leagues:
                - id: 0
                  specials:
                    - id: 0
                      status: 0
                      settlementId: 0
                      settledAt: '2017-10-11T15:05:50.996671Z'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
      deprecated: true
  /v3/fixtures/special/settled:
    get:
      tags:
        - Fixtures
      summary: Get Settled Special Fixtures - v3
      description: Returns all specials which are settled in the last 24 hours for the given Sport.
      operationId: Fixtures_Specials_Settled_V3_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: sportId
          in: query
          description: Id of the sport for which to retrieve the settled specials.
          required: true
          type: integer
          format: int32
        - name: leagueIds
          in: query
          description: Array of leagueIds. This is optional parameter.
          required: false
          type: array
          items:
            type: integer
            format: int32
          collectionFormat: multi
        - name: since
          in: query
          description: This is used to receive incremental updates. Use the value of last from previous response.
          required: false
          type: integer
          format: int64
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/SettledSpecialsResponseV3'
          examples:
            application/json:
              sportId: 0
              last: 0
              leagues:
                - id: 0
                  specials:
                    - id: 0
                      status: 0
                      settlementId: 0
                      settledAt: '2017-10-11T15:05:50.996671Z'
                      contestants:
                        - name: Barranquilla
                          outcome: "X"
                        - name: Valledupar
                          outcome: "X"  
                      cancellationReason:
                        code: string
                        details:
                          correctTeam1Id: string
                          correctTeam2Id: string
                          correctListedPitcher1: string
                          correctListedPitcher2: string
                          correctSpread: '0.0'
                          correctTotalPoints: '0.0'
                          correctTeam1TotalPoints: '0.0'
                          correctTeam2TotalPoints: '0.0'
                          correctTeam1Score: '0'
                          correctTeam2Score: '0'
                          correctTeam1TennisSetsScore: '0'
                          correctTeam2TennisSetsScore: '0'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
      deprecated: false
  /v1/odds:
    get:
      tags:
        - Odds
      summary: Get Straight Odds - v1
      description: Returns straight odds for all non-settled events. Please note that it is possible that the event is in Get Fixtures response but not in Get Odds. This happens when the odds are not currently available for wagering.
      operationId: Odds_Straight_V1_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: sportId
          in: query
          description: The sportid for which to retrieve the odds.
          required: true
          type: integer
          format: int32
        - name: leagueIds
          in: query
          description: The leagueIds array may contain a list of comma separated league ids.
          required: false
          type: array
          items:
            type: integer
            format: int32
          collectionFormat: multi
        - name: oddsFormat
          in: query
          description: Format in which we return the odds. Default is American. [American, Decimal, HongKong, Indonesian, Malay]
          required: false
          type: string
          enum:
            - American
            - Decimal
            - HongKong
            - Indonesian
            - Malay
        - name: since
          in: query
          description: This is used to receive incremental updates. Use the value of last from previous odds response. When since parameter is not provided, the odds are delayed up to 1 min to encourage the use of the parameter. Please note that when using since parameter you will get in the response ONLY changed periods. If a period did not have any changes it will not be in the response.
          required: false
          type: integer
          format: int64
        - name: isLive
          in: query
          description: To retrieve ONLY live odds set the value to 1 (isLive=1). Otherwise response will have all odds.
          required: false
          type: boolean
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/OddsResponseV1'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
      deprecated: true
  /v3/odds:
    get:
      tags:
        - Odds
      summary: Get Straight Odds - v3
      description: Returns straight odds for all non-settled events. Please note that it is possible that the event is in Get Fixtures response but not in Get Odds. This happens when the odds are not currently available for wagering.
      operationId: Odds_Straight_V3_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: sportId
          in: query
          description: The sportid for which to retrieve the odds.
          required: true
          type: integer
          format: int32
        - name: leagueIds
          in: query
          description: The leagueIds array may contain a list of comma separated league ids.
          required: false
          type: array
          items:
            type: integer
            format: int32
          collectionFormat: multi
        - name: oddsFormat
          in: query
          description: Format in which we return the odds. Default is American. [American, Decimal, HongKong, Indonesian, Malay]
          required: false
          type: string
          enum:
            - American
            - Decimal
            - HongKong
            - Indonesian
            - Malay
        - name: since
          in: query
          description: This is used to receive incremental updates. Use the value of last from previous odds response. When since parameter is not provided, the odds are delayed up to 1 min to encourage the use of the parameter. Please note that when using since parameter you will get in the response ONLY changed periods. If a period did not have any changes it will not be in the response.
          required: false
          type: integer
          format: int64
        - name: isLive
          in: query
          description: To retrieve ONLY live odds set the value to 1 (isLive=1). Otherwise response will have all odds.
          required: false
          type: boolean
        - name: eventIds
          in: query
          description: Filter by EventIds
          required: false
          type: array
          items:
            type: integer
            format: int64
          collectionFormat: multi
        - name: toCurrencyCode
          in: query
          description: 3 letter currency code as in the [/currency](https://ps3838api.github.io/docs/?api=lines#tag/Others/operation/Currencies_V2_Get) response. Limits will be returned in the requested currency. Default is USD. 
          required: false
          type: string
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/OddsResponseV3'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
  /v1/odds/parlay:
    get:
      tags:
        - Odds
      summary: Get Parlay Odds - v1
      description: Returns parlay odds for all non-settled events. Please note that it is possible that the event is in Get Fixtures response but notin Get Odds. This happens when the odds are not currently available for wagering.
      operationId: Odds_Parlays_V1_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: sportId
          in: query
          description: The sportid for which to retrieve the odds.
          required: true
          type: integer
          format: int32
        - name: leagueIds
          in: query
          description: The leagueIds array may contain a list of comma separated league ids.
          required: false
          type: array
          items:
            type: integer
            format: int32
          collectionFormat: multi
        - name: oddsFormat
          in: query
          description: Format in which we return the odds. Default is American. [American, Decimal, HongKong, Indonesian, Malay]
          required: false
          type: string
          enum:
            - American
            - Decimal
            - HongKong
            - Indonesian
            - Malay
        - name: since
          in: query
          description: This is used to receive incremental updates. Use the value of last from previous odds response. When since parameter is not provided, the odds are delayed up to 1 min to encourage the use of the parameter. Please note that when using since parameter you will get in the response ONLY changed periods. If a period didn’t have any changes it will not be in the response.
          required: false
          type: integer
          format: int64
        - name: isLive
          in: query
          description: To retrieve ONLY live odds set the value to 1 (isLive=1). Otherwise response will have all odds.
          required: false
          type: boolean
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/ParlayOddsResponseV1'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
      deprecated: true
  /v3/odds/parlay:
    get:
      tags:
        - Odds
      summary: Get Parlay Odds - v3
      description: Returns parlay odds for all non-settled events. Please note that it is possible that the event is in Get Fixtures response but notin Get Odds. This happens when the odds are not currently available for wagering.
      operationId: Odds_Parlays_V3_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: sportId
          in: query
          description: The sportid for which to retrieve the odds.
          required: true
          type: integer
          format: int32
        - name: leagueIds
          in: query
          description: The leagueIds array may contain a list of comma separated league ids.
          required: false
          type: array
          items:
            type: integer
            format: int32
          collectionFormat: multi
        - name: oddsFormat
          in: query
          description: Format in which we return the odds. Default is American. [American, Decimal, HongKong, Indonesian, Malay]
          required: false
          type: string
          enum:
            - American
            - Decimal
            - HongKong
            - Indonesian
            - Malay
        - name: since
          in: query
          description: This is used to receive incremental updates. Use the value of last from previous odds response. When since parameter is not provided, the odds are delayed up to 1 min to encourage the use of the parameter. Please note that when using since parameter you will get in the response ONLY changed periods. If a period didn’t have any changes it will not be in the response.
          required: false
          type: integer
          format: int64
        - name: isLive
          in: query
          description: To retrieve ONLY live odds set the value to 1 (isLive=1). Otherwise response will have all odds.
          required: false
          type: boolean
        - name: eventIds
          in: query
          description: Filter by EventIds
          required: false
          type: array
          items:
            type: integer
            format: int64
          collectionFormat: multi
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/ParlayOddsResponseV3'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
  /v1/odds/teaser:
    get:
      tags:
        - Odds
      summary: Get Teaser Odds - v1
      description: Returns odds for specified teaser.
      operationId: Odds_Teasers_V1_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: teaserId
          in: query
          description: Unique identifier.Teaser details can be retrieved from a call to Get Teaser Groups endpoint.
          required: true
          type: integer
          format: int64
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/TeaserOddsResponse'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
  /v1/odds/special:
    get:
      tags:
        - Odds
      summary: Get Special Odds - v1
      description: Returns odds for specials for all non-settled events.
      operationId: Odds_Special_V1_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: oddsFormat
          in: query
          description: Format the odds are returned in. [American, Decimal, HongKong, Indonesian, Malay]
          required: false
          type: string
          enum:
            - American
            - Decimal
            - HongKong
            - Indonesian
            - Malay
        - name: sportId
          in: query
          description: Id of a sport for which to retrieve the specials.
          required: true
          type: integer
          format: int32
        - name: leagueIds
          in: query
          description: The leagueIds array may contain a list of comma separated league ids.
          required: false
          type: array
          items:
            type: integer
            format: int32
          collectionFormat: multi
        - name: since
          in: query
          description: This is used to receive incremental updates. Use the value of last from previous response. When since parameter is not provided, the fixtures are delayed up to 1 min to encourage the use of the parameter.
          required: false
          type: integer
          format: int64
        - name: specialId
          in: query
          description: Id of the special. This is an optional argument.
          required: false
          type: integer
          format: int64
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/SpecialOddsResponse'
          examples:
            application/json:
              sportId: 4
              last: 636433059510590700
              leagues:
                - id: 487
                  specials:
                    - id: 1
                      maxBet: 100
                      contestantLines:
                        - id: 1
                          lineId: 1001
                          price: -199
                          handicap: null
                        - id: 2
                          lineId: 1002
                          price: -198
                          handicap: null
                    - id: 7
                      maxBet: 100
                      contestantLines:
                        - id: 13
                          lineId: 1013
                          price: -187
                          handicap: null
                        - id: 14
                          lineId: 1014
                          price: -186
                          handicap: null
                - id: 578
                  specials:
                    - id: 10
                      maxBet: 100
                      contestantLines:
                        - id: 21
                          lineId: 1021
                          price: -179
                          handicap: null
                        - id: 22
                          lineId: 1022
                          price: -178
                          handicap: null
                        - id: 23
                          lineId: 1023
                          price: -177
                          handicap: null
                        - id: 24
                          lineId: 1024
                          price: -176
                          handicap: null
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
      deprecated: true
  /v2/odds/special:
    get:
      tags:
        - Odds
      summary: Get Special Odds - v2
      description: Returns odds for specials for all non-settled events.
      operationId: Odds_Special_V2_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: oddsFormat
          in: query
          description: Format the odds are returned in. [American, Decimal, HongKong, Indonesian, Malay]
          required: false
          type: string
          enum:
            - American
            - Decimal
            - HongKong
            - Indonesian
            - Malay
        - name: sportId
          in: query
          description: Id of a sport for which to retrieve the specials.
          required: true
          type: integer
          format: int32
        - name: leagueIds
          in: query
          description: The leagueIds array may contain a list of comma separated league ids.
          required: false
          type: array
          items:
            type: integer
            format: int32
          collectionFormat: multi
        - name: since
          in: query
          description: This is used to receive incremental updates. Use the value of last from previous response. When since parameter is not provided, the fixtures are delayed up to 1 min to encourage the use of the parameter.
          required: false
          type: integer
          format: int64
        - name: specialId
          in: query
          description: Id of the special. This is an optional argument.
          required: false
          type: integer
          format: int64
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/SpecialOddsResponse'
          examples:
            application/json:
              sportId: 4
              last: 636433059510590700
              leagues:
                - id: 487
                  specials:
                    - id: 1
                      maxBet: 100
                      contestantLines:
                        - id: 1
                          lineId: 1001
                          price: -199
                          handicap: null
                        - id: 2
                          lineId: 1002
                          price: -198
                          handicap: null
                    - id: 7
                      maxBet: 100
                      contestantLines:
                        - id: 13
                          lineId: 1013
                          price: -187
                          handicap: null
                        - id: 14
                          lineId: 1014
                          price: -186
                          handicap: null
                - id: 578
                  specials:
                    - id: 10
                      maxBet: 100
                      contestantLines:
                        - id: 21
                          lineId: 1021
                          price: -179
                          handicap: null
                        - id: 22
                          lineId: 1022
                          price: -178
                          handicap: null
                        - id: 23
                          lineId: 1023
                          price: -177
                          handicap: null
                        - id: 24
                          lineId: 1024
                          price: -176
                          handicap: null
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
      deprecated: false      
  /v1/line:
    get:
      tags:
        - Line
      summary: Get Straight Line - v1
      description: Returns latest line.
      operationId: Line_Straight_V1_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: leagueId
          in: query
          description: League Id.
          required: true
          type: integer
          format: int32
        - name: handicap
          in: query
          description: This is needed for SPREAD, TOTAL_POINTS and TEAM_TOTAL_POINTS bet types
          required: true
          type: number
          format: double
        - name: oddsFormat
          in: query
          description: Format in which we return the odds. Default is American.
          required: true
          type: string
          enum:
            - American
            - Decimal
            - HongKong
            - Indonesian
            - Malay
        - name: sportId
          in: query
          description: Sport identification
          required: true
          type: integer
          format: int32
        - name: eventId
          in: query
          description: Event identification
          required: true
          type: integer
          format: int64
        - name: periodNumber
          in: query
          description: This represents the period of the match. For example, for soccer we have 0 (Game),  1 (1st Half) & 2 (2nd Half)
          required: true
          type: integer
          format: int32
        - name: betType
          in: query
          description: Bet Type
          required: true
          type: string
          enum:
            - SPREAD
            - MONEYLINE
            - TOTAL_POINTS
            - TEAM_TOTAL_POINTS
        - name: team
          in: query
          description: Chosen team type. This is needed only for SPREAD, MONEYLINE and TEAM_TOTAL_POINTS bet types
          required: false
          type: string
          enum:
            - Team1
            - Team2
            - Draw
        - name: side
          in: query
          description: Chosen side. This is needed only for TOTAL_POINTS and TEAM_TOTAL_POINTS
          required: false
          type: string
          enum:
            - OVER
            - UNDER
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/LineResponse'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
      deprecated: true              
  /v2/line:
    get:
      tags:
        - Line
      summary: Get Straight Line - v2
      description: Returns latest line.
      operationId: Line_Straight_V2_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: leagueId
          in: query
          description: League Id.
          required: true
          type: integer
          format: int32
        - name: handicap
          in: query
          description: This is needed for SPREAD, TOTAL_POINTS and TEAM_TOTAL_POINTS bet types
          required: true
          type: number
          format: double
        - name: oddsFormat
          in: query
          description: Format in which we return the odds. Default is American.
          required: true
          type: string
          enum:
            - American
            - Decimal
            - HongKong
            - Indonesian
            - Malay
        - name: sportId
          in: query
          description: Sport identification
          required: true
          type: integer
          format: int32
        - name: eventId
          in: query
          description: Event identification
          required: true
          type: integer
          format: int64
        - name: periodNumber
          in: query
          description: This represents the period of the match. Please check Get Periods endpoint for the list of currently supported periods per sport.
          required: true
          type: integer
          format: int32
        - name: betType
          in: query
          description: Bet Type
          required: true
          type: string
          enum:
            - SPREAD
            - MONEYLINE
            - TOTAL_POINTS
            - TEAM_TOTAL_POINTS
        - name: team
          in: query
          description: Chosen team type. This is needed only for SPREAD, MONEYLINE and TEAM_TOTAL_POINTS bet types
          required: false
          type: string
          enum:
            - Team1
            - Team2
            - Draw
        - name: side
          in: query
          description: Chosen side. This is needed only for TOTAL_POINTS and TEAM_TOTAL_POINTS
          required: false
          type: string
          enum:
            - OVER
            - UNDER
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/LineResponseV2'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'            
  /v1/line/parlay:
    post:
      tags:
        - Line
      summary: Get Parlay Line - v1
      description: Returns parlay lines and calculate odds.
      operationId: Line_Parlay_V1_Post
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - in: body
          name: request
          required: true
          schema:
            $ref: '#/definitions/ParlayLinesRequest'
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/ParlayLinesResponse'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
      deprecated: true              
  /v2/line/parlay:
    post:
      tags:
        - Line
      summary: Get Parlay Line - v2
      description: Returns parlay lines and calculate odds.
      operationId: Line_Parlay_V2_Post
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - in: body
          name: request
          required: true
          schema:
            $ref: '#/definitions/ParlayLinesRequestV2'
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/ParlayLinesResponseV2'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'            
  /v1/line/teaser:
    post:
      tags:
        - Line
      summary: Get Teaser Line - v1
      description: Validates a teaser bet prior to submission. Returns bet limit and price on success.
      operationId: Line_Teaser_V1_Post
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - in: body
          name: teaserLinesRequest
          required: true
          schema:
            $ref: '#/definitions/LinesRequestTeaser'
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/TeaserLinesResponse'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
  /v1/line/special:
    get:
      tags:
        - Line
      operationId: Line_Special_V1_Get
      summary: Get Special Line - v1
      description: Returns special lines and calculate odds.
      consumes: []
      produces:
        - application/json
      parameters:
        - name: oddsFormat
          in: query
          description: Format the odds are returned in. [American, Decimal, HongKong, Indonesian, Malay]
          required: true
          type: string
          enum:
            - American
            - Decimal
            - HongKong
            - Indonesian
            - Malay
        - name: specialId
          in: query
          description: Id of the special.
          required: true
          type: integer
          format: int64
        - name: contestantId
          in: query
          description: Id of the contestant.
          required: true
          type: integer
          format: int64
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/SpecialLineResponse'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
      deprecated: true
  /v2/line/special:
    get:
      tags:
        - Line
      operationId: Line_Special_V2_Get
      summary: Get Special Line - v2
      description: Returns special lines and calculate odds.
      consumes: []
      produces:
        - application/json
      parameters:
        - name: oddsFormat
          in: query
          description: Format the odds are returned in. [American, Decimal, HongKong, Indonesian, Malay]
          required: true
          type: string
          enum:
            - American
            - Decimal
            - HongKong
            - Indonesian
            - Malay
        - name: specialId
          in: query
          description: Id of the special.
          required: true
          type: integer
          format: int64
        - name: contestantId
          in: query
          description: Id of the contestant.
          required: true
          type: integer
          format: int64
        - name: handicap
          in: query
          description: handicap of the contestant. As contestant's handicap is a mutable property, it may happened that line/special returns status:SUCCESS, but with the different handicap from the one that client had at the moment of calling the line/special. One can specify handicap parameter in the request and if the contestant's handicap changed, it would return status:NOT_EXISTS. This way line/special is more aligned to how /line works.
          required: false
          type: number
          format: double  
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/SpecialLineResponse'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
      deprecated: false      
  /v1/sports:
    get:
      tags:
        - Others  
      summary: Get Sports - v1
      description: Returns all sports with the status whether they currently have lines or not.
      operationId: Sports_V1_Get
      consumes: []
      produces:
        - application/json
      parameters: []
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/SportsResponseV1'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/LinesErrorResponse'
      deprecated: true
  /v3/sports:
    get:
      tags:
        - Others  
      summary: Get Sports - v3
      description: Returns all sports with the status whether they currently have lines or not.
      operationId: Sports_V3_Get
      consumes: []
      produces:
        - application/json
      parameters: []
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/SportsResponseV3'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/LinesErrorResponse'
  /v1/leagues:
    get:
      tags:
        - Others
      summary: Get Leagues - v1
      description: Returns all sports leagues with the status whether they currently have lines or not.
      operationId: Leagues_V1_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: sportId
          in: query
          description: Sport id for which the leagues are requested.
          required: true
          type: string
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/LeaguesV1'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
      deprecated: true    
  /v3/leagues:
    get:
      tags:
        - Others
      summary: Get Leagues - v3
      description: Returns all sports leagues with the status whether they currently have lines or not.
      operationId: Leagues_V3_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: sportId
          in: query
          description: Sport id for which the leagues are requested.
          required: true
          type: string
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/LeaguesV3'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
  /v1/periods:
    get:
      tags:
        - Others
      summary: Get Periods - v1
      description: Returns all periods for a given sport.
      operationId: Periods_V1_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: sportId
          in: query
          required: true
          type: string
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/SportPeriod'
          examples:
            application/json:
              periods:
                - number: 0
                  description: Match
                  shortDescription: FT
                  spreadDescription: Handicap
                  moneylineDescription: 1X2
                  totalDescription: Total
                  team1TotalDescription: Team 1 Goals
                  team2TotalDescription: Team 2 Goals
                  spreadShortDescription: HDP
                  moneylineShortDescription: 1X2
                  totalShortDescription: O/U
                  team1TotalShortDescription: Team 1 Goals
                  team2TotalShortDescription: Team 2 Goals
                - number: 1
                  description: 1st Half
                  shortDescription: 1st H
                  spreadDescription: 1H Handicap
                  moneylineDescription: 1H 1X2
                  totalDescription: 1H Total
                  team1TotalDescription: 1H Team 1 Goals
                  team2TotalDescription: 1H Team 2 Goals
                  spreadShortDescription: 1H HDP
                  moneylineShortDescription: 1H 1X2
                  totalShortDescription: 1H O/U
                  team1TotalShortDescription: 1H GOAL
                  team2TotalShortDescription: 1H GOAL
                - number: 2
                  description: 2nd Half
                  shortDescription: 2nd H
                  spreadDescription: 2H Handicap
                  moneylineDescription: 2H 1X2
                  totalDescription: 2H Total
                  team1TotalDescription: 2H Team 1 Goals
                  team2TotalDescription: 2H Team 2 Goals
                  spreadShortDescription: 2H HDP
                  moneylineShortDescription: 2H 1X2
                  totalShortDescription: 2H O/U
                  team1TotalShortDescription: 2H GOAL
                  team2TotalShortDescription: 2H GOAL
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
  /v1/inrunning:
    get:
      tags:
        - Others
      summary: Get In-Running - v1
      description: Returns all live soccer events that have a status that indicates the event is in progress.
      operationId: InRunning_V1_Get
      consumes: []
      produces:
        - application/json
      parameters: []
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/InRunningResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedLinesErrorResponse'
      deprecated: true            
  /v2/inrunning:
    get:
      tags:
        - Others
      summary: Get In-Running - v2
      description: Returns all live soccer events that have a status that indicates the event is in progress.
      operationId: InRunning_V2_Get
      consumes: []
      produces:
        - application/json
      parameters: []
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/InRunningResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedLinesErrorResponse'
  /v1/teaser/groups:
    get:
      tags:
        - Others
      summary: Get Teaser Groups - v1
      description: Returns all teaser groups.
      operationId: Teaser_Groups_V1_Get
      consumes: []
      produces:
        - application/json
      parameters:
        - name: oddsFormat
          in: query
          description: Format the odds are returned in. [American, Decimal, HongKong, Indonesian, Malay]
          required: true
          type: string
          enum:
            - American
            - Decimal
            - HongKong
            - Indonesian
            - Malay
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/TeaserGroupsResponse'
        '400':
          description: BadRequest
          schema:
            $ref: '#/definitions/ErrorResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
  /v1/cancellationreasons:
    get:
      tags:
        - Others
      summary: Get Cancellation Reasons - v1
      description: Lookup for all the cancellation reasons
      operationId: CancellationReasons_V1_Get
      consumes: []
      produces:
        - application/json
      parameters: []
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/CancellationReasonResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
  /v2/currencies:
    get:
      tags:
        - Others
      summary: Get Currencies - v2
      description: Returns the list of supported currencies
      operationId: Currencies_V2_Get
      consumes: []
      produces:
        - application/json
      parameters: []
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/SuccessfulCurrenciesResponse'
        '401':
          description: Unauthorized
          schema:
            $ref: '#/definitions/ErrorResponse'
        '403':
          description: Forbidden
          schema:
            $ref: '#/definitions/ErrorResponse'
        '500':
          description: InternalServerError
          schema:
            $ref: '#/definitions/ExtendedErrorResponse'
securityDefinitions:
  basicAuth:
    type: basic
definitions:
  ErrorResponse:
    type: object
    properties:
      code:
        type: string
        description: Identifier representing the type of error that occurred.
      message:
        type: string
        description: Description of the error.
    description: Contains details of an error that was encountered.
  ExtendedErrorResponse:
    type: object
    properties:
      ref:
        type: string
      code:
        type: string
      message:
        type: string
  LinesErrorResponse:
    type: object
    properties:
      status:
        type: string
      error:
        $ref: '#/definitions/ErrorResponse'
      code:
        type: integer
        format: int32
        description: Code identifying an error that occurred.
  ExtendedLinesErrorResponse:
    type: object
    properties:
      ref:
        type: string
      status:
        type: string
      error:
        $ref: '#/definitions/ErrorResponse'
      code:
        type: integer
        format: int32
        description: Code identifying an error that occurred.
  CancellationReasonResponse:
    type: object
    properties:
      cancellationReasons:
        type: array
        description: Contains a list of Cancellation Reasons.
        items:
          $ref: '#/definitions/CancellationReason'
    description: Cancellation Response Data
  CancellationReason:
    type: object
    properties:
      code:
        type: string
        description: Cancellation code assigned by the server
        example: FBS_CW_65
      description:
        type: string
        description: Text description for the cancellation reason
        example: The event was postponed
    description: Cancellation Data
  SuccessfulCurrenciesResponse:
    type: object
    properties:
      currencies:
        type: array
        description: Currencies container.
        items:
          $ref: '#/definitions/Currency'
  Currency:
    type: object
    properties:
      code:
        type: string
        description: Currency code.
        example: AED
      name:
        type: string
        description: Currency name.
        example: United Arab Emirates Dirham
      rate:
        type: number
        format: double
        description: Exchange rate to USD.
        example: 3.6738
  FixturesResponseV1:
    type: object
    properties:
      sportId:
        type: integer
        format: int32
        description: Same as requested sport Id.
      last:
        type: integer
        format: int64
        description: Use this value for the subsequent requests for since query parameter to get just the changes since previous response.
      league:
        type: array
        description: Contains a list of Leagues.
        items:
          $ref: '#/definitions/FixturesLeagueV1'
  FixturesLeagueV1:
    type: object
    properties:
      id:
        type: integer
        format: int32
        description: League ID.
      events:
        type: array
        description: Contains a list of events.
        items:
          $ref: '#/definitions/FixtureV1'
  FixtureV1:
    type: object
    properties:
      id:
        type: integer
        format: int64
        description: Event id.
      starts:
        type: string
        format: date-time
        description: Start time of the event in UTC.
      home:
        type: string
        description: Home team name.
      away:
        type: string
        description: Away team name.
      rotNum:
        type: string
        description: Team1 rotation number. Please note that in the next version of /fixtures, rotNum property will be decomissioned. ParentId can be used instead to group the related events.
      liveStatus:
        type: integer
        format: int32
        description: |
          Indicates live status of the event. 
          
          0 = No live betting will be offered on this event, 
          1 = Live betting event, 
          2 = Live betting will be offered on this event
        enum:
          - 0
          - 1
          - 2
      homePitcher:
        type: string
        description: Home team pitcher. Only for Baseball.
      awayPitcher:
        type: string
        description: Away team pitcher. Only for Baseball.
      status:
        type: string
        description: |
        
          Status of the event. 
          
          O = This is the starting status of a game. It means that the lines are open for betting, 
          H = This status indicates that the lines are temporarily unavailable for betting, 
          I = This status indicates that one or more lines have a red circle (lower maximum bet amount)
        enum:
          - O
          - H
          - I
      parlayRestriction:
        type: integer
        format: int32
        description: |
        
          Parlay status of the event. 
          
          0 = Allowed to parlay, without restrictions, 
          1 = Not allowed to parlay this event, 
          2 = Allowed to parlay with the restrictions. You can not have more than one leg from the same event in the parlay. All events with the same rotation number are treated as same event.
        enum:
          - 0
          - 1
          - 2
  FixturesResponseV3:
    type: object
    properties:
      sportId:
        type: integer
        format: int32
        description: Same as requested sport Id.
      last:
        type: integer
        format: int64
        description: Use this value for the subsequent requests for since query parameter to get just the changes since previous response.
      league:
        type: array
        description: Contains a list of Leagues.
        items:
          $ref: '#/definitions/FixturesLeagueV3'
  FixturesLeagueV3:
    type: object
    properties:
      id:
        type: integer
        format: int32
        description: League ID.
      name:
        type: string
        description: League Name.
      events:
        type: array
        description: Contains a list of events.
        items:
          $ref: '#/definitions/FixtureV3'
  FixtureV3:
    type: object
    properties:
      id:
        type: integer
        format: int64
        description: Event id.
      parentId:
        type: integer
        format: int64
        description: If event is linked to another event, parentId will be populated.  Live event would have pre game event as parent id.
      starts:
        type: string
        format: date-time
        description: Start time of the event in UTC.
      home:
        type: string
        description: Home team name.
      away:
        type: string
        description: Away team name.
      rotNum:
        type: string
        description: Team1 rotation number. Please note that in the next version of /fixtures, rotNum property will be decommissioned. ParentId can be used instead to group the related events.
      liveStatus:
        type: integer
        format: int32
        description: |
          Indicates live status of the event. 
          
          0 = No live betting will be offered on this event, 
          1 = Live betting event, 
          2 = Live betting will be offered on this event
        enum:
          - 0
          - 1
          - 2
      homePitcher:
        type: string
        description: Home team pitcher. Only for Baseball.
      awayPitcher:
        type: string
        description: Away team pitcher. Only for Baseball.
      status:
        type: string
        description: |
        
          This is deprecated parameter, please check period's `status` in the
            `/odds` endpoint to see if it's open for betting.
          
          O = This is the starting status of a game. It means that the lines are open for betting, 
          H = This status indicates that the lines are temporarily unavailable for betting, 
          I = This status indicates that one or more lines have a red circle (lower maximum bet amount)
        enum:
          - O
          - H
          - I
        deprecated: true  
      betAcceptanceType:
        type: integer
        format: int32
        description: |
        
          Soccer live event bet acceptance type. This type indicates that the live soccer event is offered to the corresponding customer.
          
          0 = Not Applicable. No bet acceptance type restriction.
          1 = Danger Zone.
          2 = Live Delay.
          3 = Both.
        enum:
          - 0
          - 1
          - 2
          - 3
      parlayRestriction:
        type: integer
        format: int32
        description: |
        
          Parlay status of the event. 
          
          0 = Allowed to parlay, without restrictions, 
          1 = Not allowed to parlay this event, 
          2 = Allowed to parlay with the restrictions. You cannot have more than one leg from the same event in the parlay. All events with the same rotation number are treated as same event.
        enum:
          - 0
          - 1
          - 2
      altTeaser:
        type: boolean
        description: Whether an event is offer with alternative teaser points. Events with alternative teaser points may vary from teaser definition. 
      resultingUnit:   
        type: string
        description: | 
          Specifies based on what the event will be resulted, e.g. Corners, Bookings
      version:
        type: integer
        format: int64
        description: |
           Fixture version, goes up when there is a change in the fixture.
  SettledFixturesSportV1:
    type: object
    properties:
      sportId:
        type: integer
        format: int32
        description: Same as requested sport Id.
      last:
        type: integer
        format: int64
        description: Use this value for the subsequent requests for since query parameter to get just the changes since previous response.
      leagues:
        type: array
        description: Contains a list of Leagues.
        items:
          $ref: '#/definitions/SettledFixturesLeagueV1'
  SettledFixturesLeagueV1:
    type: object
    properties:
      id:
        type: integer
        format: int32
        description: League Id.
      events:
        type: array
        description: Contains a list of events.
        items:
          $ref: '#/definitions/SettledFixturesEventV1'
  SettledFixturesEventV1:
    type: object
    properties:
      id:
        type: integer
        format: int64
        description: Event Id.
      periods:
        type: array
        description: Contains a list of periods.
        items:
          $ref: '#/definitions/SettledFixturesPeriodV1'
  SettledFixturesPeriodV1:
    type: object
    properties:
      number:
        type: integer
        format: int32
        description: This represents the period of the match. For example, for soccer we have 0 (Game), 1 (1st Half) & 2 (2nd Half)
      status:
        type: integer
        format: int32
        description: |
          Period settlement status. 
          
          1 = Event period is settled, 
          2 = Event period is re-settled, 
          3 = Event period is cancelled, 
          4 = Event period is re-settled as cancelled, 
          5 = Event is deleted
        enum:
          - 1
          - 2
          - 3
          - 4
          - 5
      settlementId:
        type: integer
        format: int64
        description: Unique id of the settlement. In case of a re-settlement, a new settlementId and settledAt will be generated.
      settledAt:
        type: string
        format: date-time
        description: Date and time in UTC when the period was settled.
      team1Score:
        type: integer
        format: int32
        description: Team1 score.
      team2Score:
        type: integer
        format: int32
        description: Team2 score.
  SettledFixturesSportV3:
    type: object
    properties:
      sportId:
        type: integer
        format: int32
        description: Same as requested sport Id.
      last:
        type: integer
        format: int64
        description: Use this value for the subsequent requests for since query parameter to get just the changes since previous response.
      leagues:
        type: array
        description: Contains a list of Leagues.
        items:
          $ref: '#/definitions/SettledFixturesLeagueV3'
  SettledFixturesLeagueV3:
    type: object
    properties:
      id:
        type: integer
        format: int32
        description: League Id.
      events:
        type: array
        description: Contains a list of events.
        items:
          $ref: '#/definitions/SettledFixturesEventV3'
  SettledFixturesEventV3:
    type: object
    properties:
      id:
        type: integer
        format: int64
        description: Event Id.
      periods:
        type: array
        description: Contains a list of periods.
        items:
          $ref: '#/definitions/SettledFixturesPeriodV3'
  SettledFixturesPeriodV3:
    type: object
    properties:
      number:
        type: integer
        format: int32
        description: This represents the period of the match. For example, for soccer we have 0 (Game), 1 (1st Half) & 2 (2nd Half)
      status:
        type: integer
        format: int32
        description: |
          Period settlement status. 
          
          1 = Event period is settled, 
          2 = Event period is re-settled, 
          3 = Event period is cancelled, 
          4 = Event period is re-settled as cancelled, 
          5 = Event is deleted
        enum:
          - 1
          - 2
          - 3
          - 4
          - 5
      settlementId:
        type: integer
        format: int64
        description: Unique id of the settlement. In case of a re-settlement, a new settlementId and settledAt will be generated.
      settledAt:
        type: string
        format: date-time
        description: Date and time in UTC when the period was settled.
      team1Score:
        type: integer
        format: int32
        description: Team1 score.
      team2Score:
        type: integer
        format: int32
        description: Team2 score.
      cancellationReason:
        $ref: '#/definitions/CancellationReasonType'
  CancellationReasonType:
    type: object
    properties:
      code:
        type: string
        description: Cancellation Reason Code
      details:
        $ref: '#/definitions/CancellationReasonDetailsType'
  CancellationReasonDetailsType:
    type: object
    properties:
      key:
        type: string
      value:
        type: string
  InRunningResponse:
    type: object
    properties:
      sports:
        type: array
        description: Sports container
        items:
          $ref: '#/definitions/InRunningSport'
  InRunningSport:
    type: object
    properties:
      id:
        type: integer
        format: int32
        description: Sport Id
      leagues:
        type: array
        description: Leagues container
        items:
          $ref: '#/definitions/InRunningLeague'
  InRunningLeague:
    type: object
    properties:
      id:
        type: integer
        format: int32
        description: League Id
      events:
        type: array
        description: Events container
        items:
          $ref: '#/definitions/InRunningEvent'
  InRunningEvent:
    type: object
    properties:
      id:
        type: integer
        format: int64
        description: Game Id
      state:
        type: integer
        format: int32
        description: |
          State of the game.
          
          1 = First half in progress, 
          2 = Half time in progress, 
          3 = Second half in progress, 
          4 = End of regular time,
          5 = First half extra time in progress, 
          6 = Extra time half time in progress, 
          7 = Second half extra time in progress, 
          8 = End of extra time, 
          9 = End of Game, 
          10 = Game is temporary suspended, 
          11 = Penalties in progress
        enum:
          - 1
          - 2
          - 3
          - 4
          - 5
          - 6
          - 7
          - 8
          - 9
          - 10
          - 11
      elapsed:
        type: integer
        format: int32
        description: Elapsed minutes
  LeaguesV1:
    type: object
    properties:
      leagues:
        type: array
        description: Leagues container
        items:
          $ref: '#/definitions/LeagueV1'
  LeagueV1:
    type: object
    properties:
      id:
        type: integer
        format: int32
        description: League Id.
      name:
        type: string
        description: Name of the league.
      homeTeamType:
        type: string
        description: Specifies whether the home team is team1 or team2. You need this information to place a bet.
      hasOfferings:
        type: boolean
        description: Whether the league currently has events or specials.
      allowRoundRobins:
        type: boolean
        description: Specifies whether you can place parlay round robins on events in this league.
  LeaguesV3:
    type: object
    properties:
      leagues:
        type: array
        description: Leagues container
        items:
          $ref: '#/definitions/LeagueV3'
  LeagueV3:
    type: object
    properties:
      id:
        type: integer
        format: int32
        description: League Id.
      name:
        type: string
        description: Name of the league.
      homeTeamType:
        type: string
        description: Specifies whether the home team is team1 or team2. You need this information to place a bet.
      hasOfferings:
        type: boolean
        description: Whether the league currently has events or specials.
      container:
        type: string
        description: Represents grouping for the league, usually a region/country
      allowRoundRobins:
        type: boolean
        description: Specifies whether you can place parlay round robins on events in this league.
      leagueSpecialsCount:
        type: integer
        format: int32
        description: Indicates how many specials are in the given league.
      eventSpecialsCount:
        type: integer
        format: int32
        description: Indicates how many game specials are in the given league.
      eventCount:
        type: integer
        format: int32
        description: Indicates how many events are in the given league.
  LineResponse:
    type: object
    properties:
      status:
        type: string
        description: If the value is NOT_EXISTS, than this will be the only parameter in the response. All other params would be empty. [SUCCESS = OK, NOT_EXISTS = Line not offered anymore]
        enum:
          - SUCCESS
          - NOT_EXISTS
      price:
        type: number
        format: double
        description: Latest price.
      lineId:
        type: integer
        format: int64
        description: Line identification needed to place a bet.
      altLineId:
        type: integer
        format: int64
        description: This would be needed to place the bet if the handicap is on alternate line, otherwise it will not be populated in the response.
      team1Score:
        type: integer
        format: int32
        description: Away team score. Applicable to soccer only.
      team2Score:
        type: integer
        format: int32
        description: Home team score. Applicable to soccer only.
      team1RedCards:
        type: integer
        format: int32
        description: Team 1 red cards. Applicable to soccer only.
      team2RedCards:
        type: integer
        format: int32
        description: Team 2 red cards. Applicable to soccer only.
      maxRiskStake:
        type: number
        format: double
        description: Maximum bettable risk amount.
      minRiskStake:
        type: number
        format: double
        description: Minimum bettable risk amount.
      maxWinStake:
        type: number
        format: double
        description: Maximum bettable win amount.
      minWinStake:
        type: number
        format: double
        description: Minimum bettable win amount.
      effectiveAsOf:
        type: string
        description: Line is effective as of this date and time in UTC.
  LineResponseV2:
    type: object
    properties:
      status:
        type: string
        description: If the value is NOT_EXISTS, than this will be the only parameter in the response. All other params would be empty. [SUCCESS = OK, NOT_EXISTS = Line not offered anymore]
        enum:
          - SUCCESS
          - NOT_EXISTS
      price:
        type: number
        format: double
        description: Latest price.
      lineId:
        type: integer
        format: int64
        description: Line identification needed to place a bet.
      altLineId:
        type: integer
        format: int64
        description: This would be needed to place the bet if the handicap is on alternate line, otherwise it will not be populated in the response.
      team1Score:
        type: integer
        format: int32
        description: Team 1 score for the period 0. Applicable to soccer only.
      team2Score:
        type: integer
        format: int32
        description: Team 2 score for the period 0. Applicable to soccer only.
      team1RedCards:
        type: integer
        format: int32
        description: Team 1 red cards for the period 0. Applicable to soccer only.
      team2RedCards:
        type: integer
        format: int32
        description: Team 2 red cards for the period 0. Applicable to soccer only.
      maxRiskStake:
        type: number
        format: double
        description: Maximum bettable risk amount.
      minRiskStake:
        type: number
        format: double
        description: Minimum bettable risk amount.
      maxWinStake:
        type: number
        format: double
        description: Maximum bettable win amount.
      minWinStake:
        type: number
        format: double
        description: Minimum bettable win amount.
      effectiveAsOf:
        type: string
        description: Line is effective as of this date and time in UTC.    
      periodTeam1Score:
        type: integer
        format: int32
        description: Team 1 score for the supported periods. Applicable to soccer only.     
      periodTeam2Score:
        type: integer
        format: int32
        description: Team 2 score for the supported periods. Applicable to soccer only.    
      periodTeam1RedCards:
        type: integer
        format: int32
        description: Team 1 red cards for the supported periods. Applicable to soccer only.   
      periodTeam2RedCards:
        type: integer
        format: int32
        description: Team 2 red cards for the supported periods. Applicable to soccer only.          
  ParlayLinesRequest:
    type: object
    properties:
      oddsFormat:
        type: string
        description: Odds in the response will be in this format. [American, Decimal, HongKong, Indonesian, Malay]
        enum:
          - American
          - Decimal
          - HongKong
          - Indonesian
          - Malay
      legs:
        type: array
        description: This is a collection of legs
        items:
          $ref: '#/definitions/ParlayLineRequest'
  ParlayLinesRequestV2:
    type: object
    properties:
      oddsFormat:
        type: string
        description: Odds in the response will be in this format. [American, Decimal, HongKong, Indonesian, Malay]
        enum:
          - American
          - Decimal
          - HongKong
          - Indonesian
          - Malay
      legs:
        type: array
        description: This is a collection of legs
        items:
          $ref: '#/definitions/ParlayLineRequestV2'          
  ParlayLineRequest:
    type: object
    properties:
      uniqueLegId:
        type: string
        description: This unique id of the leg. It used to identify and match leg in the response.
      eventId:
        type: integer
        format: int64
        description: Id of the event.
      periodNumber:
        type: integer
        format: int32
        description: This represents the period of the match. For example, for soccer we have 0 (Game), 1 (1st Half), 2 (2nd Half)
      legBetType:
        type: string
        description: Only SPREAD, MONEYLINE and TOTAL_POINTS are supported. [SPREAD, MONEYLINE, TOTAL_POINTS]
        enum:
          - SPREAD
          - MONEYLINE
          - TOTAL_POINTS
      team:
        type: string
        description: Chosen team type. This is needed only for SPREAD and MONEYLINE wager types. [Team1, Team2, Draw (MONEYLINE only)]
        enum:
          - Team1
          - Team2
          - Draw
      side:
        type: string
        description: Chosen side. This is needed only for TOTAL_POINTS wager type.  [OVER, UNDER]
        enum:
          - OVER
          - UNDER
      handicap:
        type: number
        format: double
        description: This is needed for SPREAD and TOTAL_POINTS bet type.
    required: 
      - uniqueLegId
      - eventId
      - periodNumber
      - legBetType
  ParlayLineRequestV2:
    type: object
    properties:
      uniqueLegId:
        type: string
        description: This unique id of the leg. It used to identify and match leg in the response.
      eventId:
        type: integer
        format: int64
        description: Id of the event.
      periodNumber:
        type: integer
        format: int32
        description: This represents the period of the match. For example, for soccer we have 0 (Game), 1 (1st Half), 2 (2nd Half)
      legBetType:
        type: string
        description: SPREAD, MONEYLINE, TOTAL_POINTS and TEAM_TOTAL_POINTS are supported.
        enum:
          - SPREAD
          - MONEYLINE
          - TOTAL_POINTS
          - TEAM_TOTAL_POINTS
      team:
        type: string
        description: Chosen team type. This is needed only for SPREAD and MONEYLINE wager types. [Team1, Team2, Draw (MONEYLINE only)]
        enum:
          - Team1
          - Team2
          - Draw
      side:
        type: string
        description: Chosen side. This is needed only for TOTAL_POINTS wager type.  [OVER, UNDER]
        enum:
          - OVER
          - UNDER
      handicap:
        type: number
        format: double
        description: This is needed for SPREAD and TOTAL_POINTS bet type.
    required: 
      - uniqueLegId
      - eventId
      - periodNumber
      - legBetType      
  ParlayLinesResponse:
    type: object
    properties:
      status:
        type: string
        description: Status of the parlay [VALID = Parlay is valid, PROCESSED_WITH_ERROR = Parlay contains error(s)]
        example: PROCESSED_WITH_ERROR
        enum:
          - VALID
          - PROCESSED_WITH_ERROR
      error:
        type: string
        description: INVALID_LEGS. Signifies that one or more legs are invalid. Populated only if status is PROCESSED_WITH_ERROR.
        example: INVALID_LEGS
      maxRiskStake:
        type: number
        format: double
        description: Maximum allowed stake amount.
      minRiskStake:
        type: number
        format: double
        description: Minimum allowed stake amount.
      roundRobinOptionWithOdds:
        type: array
        description: Provides array with all acceptable Round Robin options with parlay odds for that option.
        items:
          $ref: '#/definitions/RoundRobinOptionWithOdds'
      legs:
        type: array
        description: The collection of legs (the format of the object is described below).
        items:
          $ref: '#/definitions/ParlayLineLeg'
    required: 
      - status
  ParlayLinesResponseV2:
    type: object
    properties:
      status:
        type: string
        description: Status of the parlay [VALID = Parlay is valid, PROCESSED_WITH_ERROR = Parlay contains error(s)]
        example: PROCESSED_WITH_ERROR
        enum:
          - VALID
          - PROCESSED_WITH_ERROR
      error:
        type: string
        description: INVALID_LEGS. Signifies that one or more legs are invalid. Populated only if status is PROCESSED_WITH_ERROR.
        example: INVALID_LEGS
      minRiskStake:
        type: number
        format: double
        description: Minimum allowed stake amount.
      maxParlayRiskStake:
        type: number
        format: double
        description: Maximum allowed stake amount for parlay bets.
      maxRoundRobinTotalRisk:
        type: number
        format: double
        description: Maximum allowed total stake amount for all the parlay bets in the round robin.
      maxRoundRobinTotalWin:
        type: number
        format: double
        description: Maximum allowed total win amount for all the parlay bets in the round robin.      
      roundRobinOptionWithOdds:
        type: array
        description: Provides array with all acceptable Round Robin options with parlay odds for that option.
        items:
          $ref: '#/definitions/RoundRobinOptionWithOddsV2'
      legs:
        type: array
        description: The collection of legs (the format of the object is described below).
        items:
          $ref: '#/definitions/ParlayLineLeg'
    required: 
      - status      
  RoundRobinOptionWithOdds:
    type: object
    properties:
      roundRobinOption:
        type: string
        description: | 
          RoundRobinOptions  
            
            Parlay = Single parlay that include all wagers (No Round Robin),  
            TwoLegRoundRobin = Multiple parlays having 2 wagers each (round robin style),  
            ThreeLegRoundRobin = Multiple parlays having 3 wagers each (round robin style),  
            FourLegRoundRobin = Multiple parlays having 4 wagers each (round robin style),  
            FiveLegRoundRobin = Multiple parlays having 5 wagers each (round robin style),  
            SixLegRoundRobin = Multiple parlays having 6 wagers each (round robin style),  
            SevenLegRoundRobin = Multiple parlays having 7 wagers each (round robin style),   
            EightLegRoundRobin = Multiple parlays having 8 wagers each (round robin style)  
        enum:
          - Parlay
          - TwoLegRoundRobin
          - ThreeLegRoundRobin
          - FourLegRoundRobin
          - FiveLegRoundRobin
          - SixLegRoundRobin
          - SevenLegRoundRobin
          - EightLegRoundRobin
      odds:
        type: number
        format: double
        description: Parlay odds for this option.
      unroundedDecimalOdds:
        type: number
        format: double
        description: Unrounded parlay odds in decimal format to be used for calculations only
    required: 
      - roundRobinOption
      - odds
      - unroundedDecimalOdds
  RoundRobinOptionWithOddsV2:
    type: object
    properties:
      roundRobinOption:
        type: string
        description: | 
          RoundRobinOptions  
            
            Parlay = Single parlay that include all wagers (No Round Robin),  
            TwoLegRoundRobin = Multiple parlays having 2 wagers each (round robin style),  
            ThreeLegRoundRobin = Multiple parlays having 3 wagers each (round robin style),  
            FourLegRoundRobin = Multiple parlays having 4 wagers each (round robin style),  
            FiveLegRoundRobin = Multiple parlays having 5 wagers each (round robin style),  
            SixLegRoundRobin = Multiple parlays having 6 wagers each (round robin style),  
            SevenLegRoundRobin = Multiple parlays having 7 wagers each (round robin style),   
            EightLegRoundRobin = Multiple parlays having 8 wagers each (round robin style)  
        enum:
          - Parlay
          - TwoLegRoundRobin
          - ThreeLegRoundRobin
          - FourLegRoundRobin
          - FiveLegRoundRobin
          - SixLegRoundRobin
          - SevenLegRoundRobin
          - EightLegRoundRobin
      odds:
        type: number
        format: double
        description: Parlay odds for this option.
      unroundedDecimalOdds:
        type: number
        format: double
        description: Unrounded parlay odds in decimal format to be used for calculations only
      numberOfBets:
        type: number
        format: int
        description: Number of bets in the roundRobinOption.        
    required: 
      - roundRobinOption
      - odds
      - unroundedDecimalOdds      
  ParlayLineLeg:
    type: object
    properties:
      status:
        type: string
        description: Status of the request. [VALID = Valid leg, PROCESSED_WITH_ERROR = Processed with error]
        enum:
          - VALID
          - PROCESSED_WITH_ERROR
      errorCode:
        type: string
        description: |
          When Status is PROCESSED_WITH_ERROR, provides a code indicating the specific problem. 
          
            CORRELATED = The leg is correlated with another one,  
            CANNOT_PARLAY_LIVE_GAME = The wager is placed on Live game,   
            EVENT_NO_LONGER_AVAILABLE_FOR_BETTING = The event is no longer offered for Parlays,  
            EVENT_NOT_OFFERED_FOR_PARLAY = The event is not offered for Parlays,  
            LINE_DOES_NOT_BELONG_TO_EVENT = LineId does not match the EventId specified in the request,  
            WAGER_TYPE_NO_LONGER_AVAILABLE_FOR_BETTING = Wager Type no longer available for betting, 
            WAGER_TYPE_NOT_VALID_FOR_PARLAY =  Wager Type not valid for parlay,  
            WAGER_TYPE_CONFLICTS_WITH_OTHER_LEG = Wager Type conflicts with other leg  
        enum:
          
          - CORRELATED
          - CANNOT_PARLAY_LIVE_GAME
          - EVENT_NO_LONGER_AVAILABLE_FOR_BETTING
          - EVENT_NOT_OFFERED_FOR_PARLAY
          - LINE_DOES_NOT_BELONG_TO_EVENT
          - WAGER_TYPE_NO_LONGER_AVAILABLE_FOR_BETTING
          - WAGER_TYPE_NOT_VALID_FOR_PARLAY
          - WAGER_TYPE_CONFLICTS_WITH_OTHER_LEG
      legId:
        type: string
        description: Echo of the legId from the request.
      lineId:
        type: integer
        format: int64
        description: Line identification.
      altLineId:
        type: integer
        format: int64
        description: If alternate Line was requested, the Id of that line will be returned.
      price:
        type: number
        format: double
        description: Price
      correlatedLegs:
        type: array
        description: If errorCode is CORRELATED will contain legIds of all correlated legs.
        items:
          type: string
    required: 
      - legId
      - status
  LinesRequestTeaser:
    type: object
    properties:
      teaserId:
        type: integer
        format: int64
        description: Unique identifier. Teaser details can be retrieved from a call to v1/teaser/groups endpoint.
      oddsFormat:
        type: string
        description: Format the odds are returned in.. = [American, Decimal, HongKong, Indonesian, Malay]
        enum:
          - American
          - Decimal
          - HongKong
          - Indonesian
          - Malay
      legs:
        type: array
        description: Collection of Teaser Legs.
        items:
          $ref: '#/definitions/TeaserLineRequest'
    required: 
      - teaserId
      - oddsFormat
      - legs
  TeaserLineRequest:
    type: object
    properties:
      legId:
        type: string
        description: Client genereated GUID for uniquely identifying the leg.
      eventId:
        type: integer
        format: int64
        description: Unique identifier.
      periodNumber:
        type: integer
        format: int32
        description: Period of the match that is being bet on. v1/periods endpoint can be used to retrieve all periods for a sport.
      betType:
        type: string
        description: Type of bet. Currently only SPREAD and TOTAL_POINTS are supported. [SPREAD, TOTAL_POINTS]
        enum:
          - SPREAD
          - TOTAL_POINTS
      team:
        type: string
        description: Team being bet on for a spread line. [Team1, Team2]
        enum:
          - Team1
          - Team2
      side:
        type: string
        description: Side of a total line being bet on. [OVER, UNDER]
        enum:
          - OVER
          - UNDER
      handicap:
        type: number
        format: double
        description: Number of points.
    required: 
      - legId
      - eventId
      - periodNumber
      - betType
      - handicap
  TeaserLinesResponse:
    type: object
    properties:
      status:
        type: string
        description: Status of the request. [VALID = Teaser is valid, PROCESSED_WITH_ERROR = Teaser contains one or more errors] 
        example: PROCESSED_WITH_ERROR
        enum:
          - VALID
          - PROCESSED_WITH_ERROR
      errorCode:
        type: string
        description: |
          When Status is PROCESSED_WITH_ERROR, provides a code indicating the specific problem.  
             
            INVALID_LEGS = One or more of the legs is invalid,
            SAME_EVENT_ONLY_REQUIRED = Teaser specified requires that all legs are from the same event,  
            TEASER_DISABLED = Teaser has been disabled and cannot be bet on,  
            TEASER_DOES_NOT_EXIST = The teaser identifier could not be found,
            TOO_FEW_LEGS = You do not meet the minimum number of legs requirement for the teaser specified,  
            TOO_MANY_LEGS = You are above the maximum number of legs for the teaser specified,  
            UNKNOWN = An unknown error has occurred  
        enum:
          - INVALID_LEGS
          - SAME_EVENT_ONLY_REQUIRED
          - TEASER_DISABLED
          - TEASER_DOES_NOT_EXIST
          - TOO_FEW_LEGS
          - TOO_MANY_LEGS
          - UNKNOWN
      price:
        type: number
        format: double
        description: Price for the bet.
      minRiskStake:
        type: number
        format: double
        description: Minimum bet amount for WIN_RISK_TYPE.RISK.
      maxRiskStake:
        type: number
        format: double
        description: Maximum bet amount for WIN_RISK_TYPE.RISK.
      minWinStake:
        type: number
        format: double
        description: Minimum bet amount for WIN_RISK_TYPE.WIN.
      maxWinStake:
        type: number
        format: double
        description: Maximum bet amount for WIN_RISK_TYPE.WIN.
      legs:
        type: array
        description: Collection of Teaser Legs from the request.
        items:
          $ref: '#/definitions/TeaserLineLeg'
    required:
      - status
      - legs
  TeaserLineLeg:
    type: object
    properties:
      status:
        type: string
        description: Status of the request. [VALID = Teaser is valid, PROCESSED_WITH_ERROR = Teaser contains error(s)] 
        example: PROCESSED_WITH_ERROR
        enum:
          - VALID
          - PROCESSED_WITH_ERROR
      errorCode:
        type: string
        description: |
          When Status is PROCESSED_WITH_ERROR, provides a code indicating the specific problem.  
            
            EVENT_NOT_FOUND = The event specified could not be found,  
            POINTS_NO_LONGER_AVAILABLE = The points requested are no longer available. This means that the lines moved,   
            UNKNOWN = An unknown error has occured,  
            WAGER_TYPE_NOT_VALID_FOR_TEASER = The specified wager type is not valid for teasers  
        enum:
          - EVENT_NOT_FOUND
          - POINTS_NO_LONGER_AVAILABLE
          - UNKNOWN
          - WAGER_TYPE_NOT_VALID_FOR_TEASER
      legId:
        type: string
        description: Echo of the unique id for the leg from the request.
      lineId:
        type: integer
        format: int64
        description: Line identification.
    required: 
      - legId
      - status
  OddsResponseV1:
    type: object
    properties:
      sportId:
        type: integer
        format: int32
        description: Same as requested sport Id.
      last:
        type: integer
        format: int64
        description: Use this value for the subsequent requests for since query parameter to get just the changes since previous response.
      leagues:
        type: array
        description: Contains a list of Leagues.
        items:
          $ref: '#/definitions/OddsLeagueV1'
  OddsLeagueV1:
    type: object
    properties:
      id:
        type: integer
        format: int32
        description: League Id.
      events:
        type: array
        description: Contains a list of events.
        items:
          $ref: '#/definitions/OddsEventV1'
  OddsEventV1:
    type: object
    properties:
      id:
        type: integer
        format: int64
        description: Event Id.
      awayScore:
        type: number
        format: double
        description: Away team score. Only for live soccer events.
      homeScore:
        type: number
        format: double
        description: Home team score. Only for live soccer events.
      awayRedCards:
        type: integer
        format: int32
        description: Away team red cards. Only for live soccer events.
      homeRedCards:
        type: integer
        format: int32
        description: Home team red cards. Only for live soccer events.
      periods:
        type: array
        description: Contains a list of periods.
        items:
          $ref: '#/definitions/OddsPeriodV1'
  OddsPeriodV1:
    type: object
    properties:
      lineId:
        type: integer
        format: int64
        description: Line Id.
      number:
        type: integer
        format: int32
        description: This represents the period of the match. For example, for soccer we have  0 (Game), 1 (1st Half) & 2 (2nd Half)
      cutoff:
        type: string
        format: date-time
        description: Period’s wagering cut-off date in UTC.
      maxSpread:
        type: number
        format: double
        description: Maximum spread bet. Only in straight odds response.
      maxMoneyline:
        type: number
        format: double
        description: Maximum moneyline bet. Only in straight odds response.
      maxTotal:
        type: number
        format: double
        description: Maximum total points bet. Only in straight odds response.
      maxTeamTotal:
        type: number
        format: double
        description: Maximum team total points bet. Only in straight odds response.
      spreads:
        type: array
        description: Container for spread odds.
        items:
          $ref: '#/definitions/OddsSpreadV1'
      moneyline:
        $ref: '#/definitions/OddsMoneylineV1'
      totals:
        type: array
        description: Container for team total points.
        items:
          $ref: '#/definitions/OddsTotalV1'
      teamTotal:
        $ref: '#/definitions/OddsTeamTotalsV1'
  OddsSpreadV1:
    type: object
    properties:
      altLineId:
        type: integer
        format: int64
        description: This is present only if it’s alternative line.
      hdp:
        type: number
        format: double
        description: Home team handicap.
      home:
        type: number
        format: double
        description: Home team price.
      away:
        type: number
        format: double
        description: Away team price.
  OddsMoneylineV1:
    type: object
    properties:
      home:
        type: number
        format: double
        description: Away team price
      away:
        type: number
        format: double
        description: Away team price.
      draw:
        type: number
        format: double
        description: Draw price. This is present only for events we offer price for draw.
  OddsTotalV1:
    type: object
    properties:
      altLineId:
        type: integer
        format: int64
        description: This is present only if it’s alternative line.
      points:
        type: number
        format: double
        description: Total points.
      over:
        type: number
        format: double
        description: Over price.
      under:
        type: number
        format: double
        description: Under price.
  OddsTeamTotalsV1:
    type: object
    properties:
      home:
        $ref: '#/definitions/OddsTeamTotalV1'
      away:
        $ref: '#/definitions/OddsTeamTotalV1'
  OddsTeamTotalV1:
    type: object
    properties:
      points:
        type: number
        format: double
        description: Total points.
      over:
        type: number
        format: double
        description: Over price.
      under:
        type: number
        format: double
        description: Under price.
  OddsResponseV3:
    type: object
    properties:
      sportId:
        type: integer
        format: int32
        description: Same as requested sport Id.
      last:
        type: integer
        format: int64
        description: Use this value for the subsequent requests for since query parameter to get just the changes since previous response.
      leagues:
        type: array
        description: Contains a list of Leagues.
        items:
          $ref: '#/definitions/OddsLeagueV3'
  OddsLeagueV3:
    type: object
    properties:
      id:
        type: integer
        format: int32
        description: League Id.
      events:
        type: array
        description: Contains a list of events.
        items:
          $ref: '#/definitions/OddsEventV3'
  OddsEventV3:
    type: object
    properties:
      id:
        type: integer
        format: int64
        description: Event Id.
      awayScore:
        type: number
        format: double
        description: Away team score. Only for live soccer events.Supported only for full match period (number=0).
      homeScore:
        type: number
        format: double
        description: Home team score. Only for live soccer events.Supported only for full match period (number=0).
      awayRedCards:
        type: integer
        format: int32
        description: Away team red cards. Only for live soccer events. Supported only for full match period (number=0).
      homeRedCards:
        type: integer
        format: int32
        description: Home team red cards. Only for live soccer events.Supported only for full match period (number=0).
      periods:
        type: array
        description: Contains a list of periods.
        items:
          $ref: '#/definitions/OddsPeriodV3'
  OddsPeriodV3:
    type: object
    properties:
      lineId:
        type: integer
        format: int64
        description: Line Id.
      number:
        type: integer
        format: int32
        description: This represents the period of the match. For example, for soccer we have  0 (Game), 1 (1st Half) & 2 (2nd Half)
      cutoff:
        type: string
        format: date-time
        description: Period’s wagering cut-off date in UTC.
      status:
        type: integer
        format: int32
        description: |
              1 - online, period is open for betting 
              2 - offline, period is not open for betting
        example: 1
      maxSpread:
        type: number
        format: double
        description: Maximum spread bet. Only in straight odds response.
      maxMoneyline:
        type: number
        format: double
        description: Maximum moneyline bet. Only in straight odds response.
      maxTotal:
        type: number
        format: double
        description: Maximum total points bet. Only in straight odds response.
      maxTeamTotal:
        type: number
        format: double
        description: Maximum team total points bet. Only in straight odds response.
      moneylineUpdatedAt:
        type: string
        format: date-time
        description: Date time of the last moneyline update.
      spreadUpdatedAt:
        type: string
        format: date-time
        description: Date time of the last spread update.
      totalUpdatedAt:
        type: string
        format: date-time
        description: Date time of the last total update.
      teamTotalUpdatedAt:
        type: string
        format: date-time
        description: Date time of the last team total update.        
      spreads:
        type: array
        description: Container for spread odds.
        items:
          $ref: '#/definitions/OddsSpreadV3'
      moneyline:
        $ref: '#/definitions/OddsMoneylineV3'
      totals:
        type: array
        description: Container for team total points.
        items:
          $ref: '#/definitions/OddsTotalV3'
      teamTotal:
        $ref: '#/definitions/OddsTeamTotalsV3'
      awayScore:
        type: number
        format: double
        description: Period away team score. Only for live soccer events. Supported only for Match (number=0) and Extra Time (number=3).
      homeScore:
        type: number
        format: double
        description: Period home team score. Only for live soccer events. Supported only for Match (number=0) and Extra Time (number=3).
      awayRedCards:
        type: number
        format: int32
        description: Period away team red cards. Only for live soccer events. Supported only for Match (number=0) and Extra Time (number=3).
      homeRedCards:
        type: number
        format: int32
        description: Period home team red cards. Only for live soccer events. Supported only for Match (number=0) and Extra Time number=3).        
  OddsSpreadV3:
    type: object
    properties:
      altLineId:
        type: integer
        format: int64
        description: This is present only if it’s alternative line.
      hdp:
        type: number
        format: double
        description: Home team handicap.
      home:
        type: number
        format: double
        description: Home team price.
      away:
        type: number
        format: double
        description: Away team price.
      max:
        type: number
        format: double
        nullable: true
        description: Maximum bet volume. Present only on alternative lines, if set it overides `maxSpread` market limit.        
  OddsMoneylineV3:
    type: object
    properties:
      home:
        type: number
        format: double
        description: Away team price
      away:
        type: number
        format: double
        description: Away team price.
      draw:
        type: number
        format: double
        description: Draw price. This is present only for events we offer price for draw.
  OddsTotalV3:
    type: object
    properties:
      altLineId:
        type: integer
        format: int64
        description: This is present only if it’s alternative line.
      points:
        type: number
        format: double
        description: Total points.
      over:
        type: number
        format: double
        description: Over price.
      under:
        type: number
        format: double
        description: Under price.
      max:
        type: number
        format: double
        nullable: true
        description: Maximum bet volume. Present only on alternative lines, if set it overides `maxTotal` market limit.        
  OddsTeamTotalsV3:
    type: object
    properties:
      home:
        $ref: '#/definitions/OddsTeamTotalV3'
      away:
        $ref: '#/definitions/OddsTeamTotalV3'
  OddsTeamTotalV3:
    type: object
    properties:
      points:
        type: number
        format: double
        description: Total points.
      over:
        type: number
        format: double
        description: Over price.
      under:
        type: number
        format: double
        description: Under price.
  ParlayOddsResponseV1:
    type: object
    properties:
      sportId:
        type: integer
        format: int32
        description: Same as requested sport Id.
      last:
        type: integer
        format: int64
        description: Use this value for the subsequent requests for since query parameter to get just the changes since previous response.
      leagues:
        type: array
        description: Contains a list of Leagues.
        items:
          $ref: '#/definitions/ParlayOddsLeagueV1'
    required:
      - sportId
      - last
      - leagues
  ParlayOddsLeagueV1:
    type: object
    properties:
      id:
        type: integer
        format: int32
        description: League Id.
      events:
        type: array
        description: Contains a list of events.
        items:
          $ref: '#/definitions/ParlayOddsEventV1'
    required:
      - id
      - events
  ParlayOddsEventV1:
    type: object
    properties:
      id:
        type: integer
        format: int64
        description: Event Id.
      awayScore:
        type: number
        format: double
        description: Away team score. Only for live soccer events.
      homeScore:
        type: number
        format: double
        description: Home team score. Only for live soccer events.
      awayRedCards:
        type: integer
        format: int32
        description: Away team red cards. Only for live soccer events.
      homeRedCards:
        type: integer
        format: int32
        description: Home team red cards. Only for live soccer events.
      periods:
        type: array
        description: Contains a list of periods.
        items:
          $ref: '#/definitions/ParlayOddsPeriodV1'
    required:
      - id
      - periods
  ParlayOddsPeriodV1:
    type: object
    properties:
      lineId:
        type: integer
        format: int64
        description: Line Id.
      number:
        type: integer
        format: int32
        description: This represents the period of the match. For example, for soccer we have 0 (Game), 1 (1st Half) & 2 (2nd Half)
      cutoff:
        type: string
        format: date-time
        description: Period’s wagering cut-off date in UTC.
      maxSpread:
        type: number
        format: double
        description: Maximum spread bet. Only in straight odds response.
      maxMoneyline:
        type: number
        format: double
        description: Maximum moneyline bet. Only in straight odds response.
      maxTotal:
        type: number
        format: double
        description: Maximum total points bet. Only in straight odds response.
      maxTeamTotal:
        type: number
        format: double
        description: Maximum team total points bet. Only in straight odds response.
      spreads:
        type: array
        description: Container for spread odds.
        items:
          $ref: '#/definitions/ParlayOddsSpreadV1'
      moneyline:
        $ref: '#/definitions/ParlayOddsMoneylineV1'
      totals:
        type: array
        description: Container for team total points.
        items:
          $ref: '#/definitions/ParlayOddsTotalV1'
      teamTotal:
        $ref: '#/definitions/ParlayOddsTeamTotalsV1'
    required:
      - lineId
      - number
      - cutoff
  ParlayOddsSpreadV1:
    type: object
    properties:
      altLineId:
        type: integer
        format: int64
        description: This is present only if it’s alternative line.
      hdp:
        type: number
        format: double
        description: Home team handicap.
      home:
        type: number
        format: double
        description: Home team price.
      away:
        type: number
        format: double
        description: Away team price.
    required:
      - hdp
      - home
      - away
  ParlayOddsMoneylineV1:
    type: object
    properties:
      home:
        type: number
        format: double
        description: Away team price
      away:
        type: number
        format: double
        description: Away team price.
      draw:
        type: number
        format: double
        description: Draw price. This is present only for events we offer price for draw.
    required:
      - home
      - away
  ParlayOddsTotalV1:
    $ref: '#/definitions/ParlayOddsTotalsV1'
  ParlayOddsTeamTotalsV1:
    type: object
    properties:
      away:
        $ref: '#/definitions/ParlayOddsTotalsV1'
      home:
        $ref: '#/definitions/ParlayOddsTotalsV1'
  ParlayOddsTotalsV1:
    type: object
    properties:
      altLineId:
        type: number
        format: int64
        description: Line Id for the alternate line. This is present only if it’s alternative line.
      points:
        type: number
        format: double
        description: Total points.
      over:
        type: number
        format: double
        description: Over price.
      under:
        type: number
        format: double
        description: Under price.
    required:
      - points
      - over
      - under
  ParlayOddsResponseV3:
    type: object
    properties:
      sportId:
        type: integer
        format: int32
        description: Same as requested sport Id.
      last:
        type: integer
        format: int64
        description: Use this value for the subsequent requests for since query parameter to get just the changes since previous response.
      leagues:
        type: array
        description: Contains a list of Leagues.
        items:
          $ref: '#/definitions/ParlayOddsLeagueV3'
    required:
      - sportId
      - last
      - leagues
  ParlayOddsLeagueV3:
    type: object
    properties:
      id:
        type: integer
        format: int32
        description: League Id.
      events:
        type: array
        description: Contains a list of events.
        items:
          $ref: '#/definitions/ParlayOddsEventV3'
    required:
      - id
      - events
  ParlayOddsEventV3:
    type: object
    properties:
      id:
        type: integer
        format: int64
        description: Event Id.
      awayScore:
        type: number
        format: double
        description: Away team score. Only for live soccer events.
      homeScore:
        type: number
        format: double
        description: Home team score. Only for live soccer events.
      awayRedCards:
        type: integer
        format: int32
        description: Away team red cards. Only for live soccer events.
      homeRedCards:
        type: integer
        format: int32
        description: Home team red cards. Only for live soccer events.
      periods:
        type: array
        description: Contains a list of periods.
        items:
          $ref: '#/definitions/ParlayOddsPeriodV3'
    required:
      - id
      - periods
  ParlayOddsPeriodV3:
    type: object
    properties:
      lineId:
        type: integer
        format: int64
        description: Line Id.
      number:
        type: integer
        format: int32
        description: This represents the period of the match. For example, for soccer we have 0 (Game), 1 (1st Half) & 2 (2nd Half)
      cutoff:
        type: string
        format: date-time
        description: Period’s wagering cut-off date in UTC.
      status:
        type: integer
        format: int32
        description: |
              1 - online, period is open for betting 
              2 - offline, period is not open for betting
        example: 1  
      maxSpread:
        type: number
        format: double
        description: Maximum spread bet. Only in straight odds response.
      maxMoneyline:
        type: number
        format: double
        description: Maximum moneyline bet. Only in straight odds response.
      maxTotal:
        type: number
        format: double
        description: Maximum total points bet. Only in straight odds response.
      maxTeamTotal:
        type: number
        format: double
        description: Maximum team total points bet. Only in straight odds response.
      moneylineUpdatedAt:
        type: number
        format: double
        description: Date time of the last moneyline update.
      spreadUpdatedAt:
        type: number
        format: double
        description: Date time of the last spread update.
      totalUpdatedAt:
        type: number
        format: double
        description: Date time of the last total update.
      teamTotalUpdatedAt:
        type: number
        format: double
        description: Date time of the last team total update.                
      spreads:
        type: array
        description: Container for spread odds.
        items:
          $ref: '#/definitions/ParlayOddsSpreadV3'
      moneyline:
        $ref: '#/definitions/ParlayOddsMoneylineV3'
      totals:
        type: array
        description: Container for team total points.
        items:
          $ref: '#/definitions/ParlayOddsTotalV3'
      teamTotal:
        $ref: '#/definitions/ParlayOddsTeamTotalsV3'
      awayScore:
        type: number
        format: double
        description: Period away team score. Only for live soccer events. Supported only for Match (number=0) and Extra Time (number=3).
      homeScore:
        type: number
        format: double
        description: Period home team score. Only for live soccer events. Supported only for Match (number=0) and Extra Time (number=3).
      awayRedCards:
        type: number
        format: double
        description: Period away team red cards. Only for live soccer events. Supported only for Match (number=0) and Extra Time (number=3).
      homeRedCards:
        type: number
        format: double
        description: Period home team red cards. Only for live soccer events. Supported only for Match (number=0) and Extra Time number=3).               
    required:
      - lineId
      - number
      - cutoff
  ParlayOddsSpreadV3:
    type: object
    properties:
      altLineId:
        type: integer
        format: int64
        description: This is present only if it’s alternative line.
      hdp:
        type: number
        format: double
        description: Home team handicap.
      home:
        type: number
        format: double
        description: Home team price.
      away:
        type: number
        format: double
        description: Away team price.
      max:
        type: number
        format: double
        nullable: true
        description: Maximum bet volume. Present only on alternative lines, if set it overides `maxSpread` market limit.
    required:
      - hdp
      - home
      - away
  ParlayOddsMoneylineV3:
    type: object
    properties:
      home:
        type: number
        format: double
        description: Away team price
      away:
        type: number
        format: double
        description: Away team price.
      draw:
        type: number
        format: double
        description: Draw price. This is present only for events we offer price for draw.
    required:
      - home
      - away
  ParlayOddsTotalV3:
    $ref: '#/definitions/ParlayOddsTotalsV3'
  ParlayOddsTeamTotalsV3:
    type: object
    properties:
      away:
        $ref: '#/definitions/ParlayOddsTotalsV3'
      home:
        $ref: '#/definitions/ParlayOddsTotalsV3'
  ParlayOddsTotalsV3:
    type: object
    properties:
      altLineId:
        type: number
        format: int64
        description: Line Id for the alternate line. This is present only if it’s alternative line.
      points:
        type: number
        format: double
        description: Total points.
      over:
        type: number
        format: double
        description: Over price.
      under:
        type: number
        format: double
        description: Under price.
      max:
        type: number
        format: double
        nullable: true
        description: Maximum bet volume. Present only on alternative lines, if set it overides `maxTotal` market limit.         
    required:
      - points
      - over
      - under
  TeaserOddsResponse:
    type: object
    properties:
      teaserId:
        type: integer
        format: int64
        description: Unique identifier. Teaser details can be retrieved from a call to Get Teaser Groups endpoint.
      sportId:
        type: integer
        format: int32
        description: Unique identifier. Sport details can be retrieved from a call to Get Sports endpoint.
      leagues:
        type: array
        description: A collection of League.
        items:
          $ref: '#/definitions/TeaserOddsLeague'
  TeaserOddsLeague:
    type: object
    properties:
      id:
        type: integer
        format: int32
        description: Unique identifier. League details can be retrieved from a call to Get Leagues endpoint.
      events:
        type: array
        description: A collection of Event.
        items:
          $ref: '#/definitions/TeaserOddsEvent'
  TeaserOddsEvent:
    type: object
    properties:
      id:
        type: integer
        format: int64
        description: Unique identifier.
      periods:
        type: array
        description: A collection of periods indicating the period numbers available for betting.
        items:
          $ref: '#/definitions/TeaserOddsPeriod'
  TeaserOddsPeriod:
    type: object
    properties:
      number:
        type: integer
        format: int32
        description: Period of the match that the request is for. Refer to v1/periods endpoint to retrieve all valid periods for a sport.
      lineId:
        type: integer
        format: int64
        description: Unique identifier.
      spreadUpdatedAt:
        type: string
        format: date-time
        description: Date time of the last spread update.  
      totalUpdatedAt:
        type: string
        format: date-time
        description: Date time of the last total update.          
      spread:
        $ref: '#/definitions/TeaserOddsSpread'
      total:
        $ref: '#/definitions/TeaserOddsTotalPoints'
  TeaserOddsSpread:
    type: object
    properties:
      maxBet:
        type: number
        format: double
        description: Maximum bet amount.
      homeHdp:
        type: number
        format: double
        description: Home team handicap. Refer to Get Fixtures endpoint to determine home and away teams.
      awayHdp:
        type: number
        format: double
        description: Away team handicap. Refer to Get Fixtures endpoint to determine home and away teams.
      altHdp:
        type: boolean 
        description: Whether the spread is offer with alterantive teaser points. Events with alternative teaser points may vary from teaser definition. 
        example: false  
  TeaserOddsTotalPoints:
    type: object
    properties:
      maxBet:
        type: number
        format: double
        description: Maximum bet amount.
      overPoints:
        type: number
        format: double
        description: Over points.
      underPoints:
        type: number
        format: double
        description: Under points.
  SportPeriod:
    type: object
    properties:
      number:
        type: integer
        format: int32
        description: Period Number
      description:
        type: string
        description: Description for the period
      shortDescription:
        type: string
        description: Short description for the period
      spreadDescription:
        type: string
        description: Description for the Spread
      moneylineDescription:
        type: string
        description: Description for the Moneyline
      totalDescription:
        type: string
        description: Description for the Totals
      team1TotalDescription:
        type: string
        description: Description for Team1 Totals
      team2TotalDescription:
        type: string
        description: Description for Team2 Totals
      spreadShortDescription:
        type: string
        description: Short description for the Spread
      moneylineShortDescription:
        type: string
        description: Short description for the Moneyline
      totalShortDescription:
        type: string
        description: Short description for the Totals
      team1TotalShortDescription:
        type: string
        description: Short description for Team1 Totals
      team2TotalShortDescription:
        type: string
        description: Short description for Team2 Totals
  SportsResponseV1:
    type: object
    properties:
      sports:
        type: array
        description: Sports container.
        items:
          $ref: '#/definitions/SportV1'
  SportV1:
    type: object
    properties:
      id:
        type: integer
        format: int32
        description: Sport Id.
      name:
        type: string
        description: Sport name.
      hasOfferings:
        type: boolean
        description: Whether the sport currently has events or specials.
  SportsResponseV3:
    type: object
    properties:
      sports:
        type: array
        description: Sports container.
        items:
          $ref: '#/definitions/SportV3'
  SportV3:
    type: object
    properties:
      id:
        type: integer
        format: int32
        description: Sport Id.
      name:
        type: string
        description: Sport name.
      hasOfferings:
        type: boolean
        description: Whether the sport currently has events or specials.
      leagueSpecialsCount:
        type: integer
        format: int32
        description: Indicates how many specials are in the given sport.
      eventSpecialsCount:
        type: integer
        format: int32
        description: Indicates how many event specials are in the given sport.
      eventCount:
        type: integer
        format: int32
        description: Indicates how many events are in the given sport.
  TeaserGroupsResponse:
    type: object
    properties:
      teaserGroups:
        type: array
        description: A collection of TeaserGroups containing available teasers.
        items:
          $ref: '#/definitions/TeaserGroups'
  TeaserGroups:
    type: object
    properties:
      id:
        type: integer
        format: int64
        description: Unique identifier.
      name:
        type: string
        description: Friendly name for the Teaser Group
      teasers:
        type: array
        description: A collection of Teaser.
        items:
          $ref: '#/definitions/TeaserGroupsTeaser'
  TeaserGroupsTeaser:
    type: object
    properties:
      id:
        type: integer
        format: int64
        description: Unique identifier.
      description:
        type: string
        description: Description for the Teaser.
      sportId:
        type: integer
        format: int32
        description: Unique Sport identifier. Sport details can be retrieved from a call to v2/sports endpoint.
      minLegs:
        type: integer
        format: int32
        description: Minimum number of legs that must be selected.
      maxLegs:
        type: integer
        format: int32
        description: Maximum number of legs that can be selected.
      sameEventOnly:
        type: boolean
        description: If 'true' then all legs must be from the same event, otherwise legs can be from different events.
      payouts:
        type: array
        description: A collection of Payout indicating all possible payout combinations.
        items:
          $ref: '#/definitions/TeaserGroupsPayout'
      leagues:
        type: array
        description: A collection of Leagues available to the teaser.
        items:
          $ref: '#/definitions/TeaserGroupsLeague'
  TeaserGroupsPayout:
    type: object
    properties:
      numberOfLegs:
        type: integer
        format: int32
        description: Number of legs that must be bet and won to get the associated price.
      price:
        type: number
        format: double
        description: Price of the bet given the specified number of legs.
  TeaserGroupsLeague:
    type: object
    properties:
      id:
        type: integer
        format: int32
        description: Unique identifier. League details can be retrieved from a call to v2/leagues endpoint.
      spread:
        $ref: '#/definitions/TeaserGroupsBetType'
      total:
        $ref: '#/definitions/TeaserGroupsBetType'
  TeaserGroupsBetType:
    type: object
    properties:
      points:
        type: number
        format: double
        description: Number of points the line will be teased for the given league.
  SpecialsFixturesResponse:
    type: object
    properties:
      sportId:
        format: int32
        description: Id of a sport for which to retrieve the odds.
        type: integer
      last:
        format: int64
        description: Used for retrieving changes only on subsequent requests. Provide this value as the Since paramter in subsequent calls to only retrieve changes.
        type: integer
      leagues:
        description: Contains a list of Leagues.
        type: array
        items:
          $ref: '#/definitions/SpecialsFixturesLeague'
  SpecialsFixturesResponseV2:
    type: object
    properties:
      sportId:
        format: int32
        description: Id of a sport for which to retrieve the odds.
        type: integer
      last:
        format: int64
        description: Used for retrieving changes only on subsequent requests. Provide this value as the Since paramter in subsequent calls to only retrieve changes.
        type: integer
      leagues:
        description: Contains a list of Leagues.
        type: array
        items:
          $ref: '#/definitions/SpecialsFixturesLeagueV2'          
  SpecialsFixturesLeague:
    type: object
    properties:
      id:
        format: int32
        description: FixturesLeague Id.
        type: integer
      specials:
        description: A collection of Specials
        type: array
        items:
          $ref: '#/definitions/SpecialFixture'
  SpecialsFixturesLeagueV2:
    type: object
    properties:
      id:
        format: int32
        description: FixturesLeague Id.
        type: integer
      specials:
        description: A collection of Specials
        type: array
        items:
          $ref: '#/definitions/SpecialFixtureV2'          
  SpecialFixture:
    type: object
    properties:
      id:
        format: int64
        description: Unique Id
        type: integer
      betType:
        description: The type [MULTI_WAY_HEAD_TO_HEAD, SPREAD, OVER_UNDER]
        enum:
          - MULTI_WAY_HEAD_TO_HEAD
          - SPREAD
          - OVER_UNDER
        type: string
      name:
        description: Name of the special.
        type: string
      date:
        format: date-time
        description: Date of the special in UTC.
        type: string
      cutoff:
        format: date-time
        description: Wagering cutoff date in UTC.
        type: string
      category:
        description: The category that the special falls under.
        type: string
      units:
        description: Measurment in the context of the special. This is applicable to specials bet type spead and over/under. In a hockey special this could be goals.
        type: string
      status:
        description: |
          Status of the Special 
          
          O = This is the starting status of a game. It means that the lines are open for betting, 
          H = This status indicates that the lines are temporarily unavailable for betting, 
          I = This status indicates that one or more lines have a red circle (a lower maximum bet amount)
        enum:
          - O
          - H
          - I
        type: string
      event:
        $ref: '#/definitions/SpecialsFixturesEvent'
      contestants:
        description: ContestantLines available for wagering.
        type: array
        items:
          $ref: '#/definitions/SpecialsFixturesContestant'
  SpecialFixtureV2:
    type: object
    properties:
      id:
        format: int64
        description: Unique Id
        type: integer
      betType:
        description: The type [MULTI_WAY_HEAD_TO_HEAD, SPREAD, OVER_UNDER]
        enum:
          - MULTI_WAY_HEAD_TO_HEAD
          - SPREAD
          - OVER_UNDER
        type: string
      name:
        description: Name of the special.
        type: string
      date:
        format: date-time
        description: Date of the special in UTC.
        type: string
      cutoff:
        format: date-time
        description: Wagering cutoff date in UTC.
        type: string
      category:
        description: The category that the special falls under.
        type: string
      units:
        description: Measurment in the context of the special. This is applicable to specials bet type spead and over/under. In a hockey special this could be goals.
        type: string
      status:
        description: |
          Status of the Special 
          
          O = This is the starting status of a game. It means that the lines are open for betting, 
          H = This status indicates that the lines are temporarily unavailable for betting, 
          I = This status indicates that one or more lines have a red circle (a lower maximum bet amount)
        enum:
          - O
          - H
          - I
        type: string
      event:
        $ref: '#/definitions/SpecialsFixturesEventV2'
      contestants:
        description: ContestantLines available for wagering.
        type: array
        items:
          $ref: '#/definitions/SpecialsFixturesContestant' 
      liveStatus:
        format: int32      
        description: |
          When a special is linked to an event, we will return live status of the event, otherwise it will be 0. 0 = No live betting will be offered on this event, 1 = Live betting event, 2 = Live betting will be offered on this match, but on a different event. 
          
          Please note that live delay is applied when placing bets on special with LiveStatus=1
        enum:
          - 0
          - 1
          - 2
        type: integer
  SpecialsFixturesEvent:
    type: object
    description: Optional event asscoaited with the special.
    properties:
      id:
        format: int32
        description: Event Id
        type: integer
      periodNumber:
        format: int32
        description: The period of the match. For example in soccer 0 (Game), 1 (1st Half) & 2 (2nd Half)
        type: integer
  SpecialsFixturesEventV2:
    type: object
    description: Optional event asscoaited with the special.
    properties:
      id:
        format: int32
        description: Event Id
        type: integer
      periodNumber:
        format: int32
        description: The period of the match. For example in soccer 0 (Game), 1 (1st Half) & 2 (2nd Half)
        type: integer
      home:
        description: Home team name.
        type: string
      away:
        description: Away team name.
        type: string        
  SpecialsFixturesContestant:
    type: object
    properties:
      id:
        format: int64
        description: Contestant Id.
        type: integer
      name:
        description: Name of the contestant.
        type: string
      rotNum:
        format: int32
        description: Rotation Number.
        type: integer
  SettledSpecialsResponseV1:
    description: Response dto for SettledSpecials request
    type: object
    properties:
      sportId:
        format: int32
        description: Id of a sport for which to retrieve the odds.
        type: integer
      last:
        format: int64
        description: Last index for the settled fixture
        type: integer
      leagues:
        description: List of Leagues.
        type: array
        items:
          $ref: '#/definitions/SettledSpecialsLeagueV1'
  SettledSpecialsLeagueV1:
    description: League Dto to hold all settled specials for the league
    type: object
    properties:
      id:
        format: int32
        description: League Id.
        type: integer
      specials:
        description: A collection of Settled Specials
        type: array
        items:
          $ref: '#/definitions/SettledSpecialV1'
  SettledSpecialV1:
    description: Settled Special
    type: object
    properties:
      id:
        format: int64
        description: Id for the Settled Special
        type: integer
      status:
        format: int32
        description: Status of the settled special.
        type: integer
      settlementId:
        format: int64
        description: Id for the Settled Special
        type: integer
      settledAt:
        format: date-time
        description: Settled DateTime
        type: string
  SettledSpecialsResponseV3:
    description: Response dto for SettledSpecials request
    type: object
    properties:
      sportId:
        format: int32
        description: Id of a sport for which to retrieve the odds.
        type: integer
      last:
        format: int64
        description: Last index for the settled fixture
        type: integer
      leagues:
        description: List of Leagues.
        type: array
        items:
          $ref: '#/definitions/SettledSpecialsLeagueV3'
  SettledSpecialsLeagueV3:
    description: League Dto to hold all settled specials for the league
    type: object
    properties:
      id:
        format: int32
        description: League Id.
        type: integer
      specials:
        description: A collection of Settled Specials
        type: array
        items:
          $ref: '#/definitions/SettledSpecialV3'
  SettledSpecialV3:
    description: Settled Special
    type: object
    properties:
      id:
        format: int64
        description: Id for the Settled Special
        type: integer
      status:
        format: int32
        description: Status of the settled special.
        type: integer
      settlementId:
        format: int64
        description: Id for the Settled Special
        type: integer
      settledAt:
        format: date-time
        description: Settled DateTime
        type: string
      cancellationReason:
        $ref: '#/definitions/CancellationReasonType'
        description: Cancellation Reason for Special Event
      contestants:
        description: A collection of contestants
        type: array
        items:
          $ref: '#/definitions/SettledContestants'
  SettledContestants:
    description: Settled Special
    type: object
    properties:
      name: 
        description: Contestant name
        type: string
        example: Union Magdalena
      outcome: 
        type: string
        description: |
          Contestant outcomes. 
          
          W = Won, 
          L = Lost, 
          X = Cancelled, 
          T = Tie, 
          Z = Scratched          
        enum:
          - W
          - L
          - X
          - T
          - Z
  SpecialLineResponse:
    type: object
    properties:
      status:
        description: Status [SUCCESS = OK, NOT_EXISTS = Line not offered anymore]
        enum:
          - SUCCESS
          - NOT_EXISTS
        type: string
      specialId:
        format: int64
        description: Special Id.
        type: integer
      contestantId:
        format: int64
        description: Contestant Id.
        type: integer
      minRiskStake:
        format: double
        description: Minimum bettable risk amount.
        type: number
      maxRiskStake:
        format: double
        description: Maximum bettable risk amount.
        type: number
      minWinStake:
        format: double
        description: Minimum bettable win amount.
        type: number
      maxWinStake:
        format: double
        description: Maximum bettable win amount.
        type: number
      lineId:
        format: int64
        description: Line identification needed to place a bet.
        type: integer
      price:
        format: double
        description: Latest price.
        type: number
      handicap:
        format: double
        description: Handicap.
        type: number
  SpecialOddsResponse:
    type: object
    properties:
      sportId:
        format: int32
        description: Id of a sport for which to retrieve the odds.
        type: integer
      last:
        format: int64
        description: Used for retrieving changes only on subsequent requests. Provide this value as the Since paramter in subsequent calls to only retrieve changes.
        type: integer
      leagues:
        description: Contains a list of Leagues.
        type: array
        items:
          $ref: '#/definitions/SpecialOddsLeague'
  SpecialOddsLeague:
    type: object
    properties:
      id:
        format: int32
        description: League id.
        type: integer
      specials:
        description: A collection of FixturesSpecial.
        type: array
        items:
          $ref: '#/definitions/SpecialOddsSpecial'
  SpecialOddsSpecial:
    type: object
    properties:
      id:
        format: int64
        description: Special Id.
        type: integer
      maxRisk:
        format: double
        description: Maximum risk amount.
        type: number
      contestantLines:
        description: ContestantLines available for wagering on.
        type: array
        items:
          $ref: '#/definitions/SpecialOddsContestantLine'
  SpecialOddsContestantLine:
    type: object
    properties:
      id:
        format: int64
        description: ContestantLine Id.
        type: integer
      lineId:
        format: int64
        description: Line identifier required for placing a bet.
        type: integer
      price:
        format: double
        description: Price of the line.
        type: number
      handicap:
        format: double
        description: 'A number indicating the spread, over/under etc.'
        type: number
